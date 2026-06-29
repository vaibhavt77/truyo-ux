# Truyo Silo Extension - Product Requirements Document

## 1. Executive Summary

The Silo Extension introduces a multi-context data segmentation model within the Truyo platform, enabling a single consumer identity (e.g., email address) to maintain independent data scopes across:

- Preferences
- Consent
- Data privacy requests

This is implemented via a new key: Silo ID, extending the existing lookup model.

---

## 2. Data Model Overview

### 2.1 Current Model
```
OrgID + ConsumerKey
```

### 2.2 New Model
```
OrgID + ConsumerKey + SiloID
```

### 2.3 Silo Definition

| Attribute | Type | Rules |
|-----------|------|-------|
| SiloID | string | Required, unique per org |
| Deletable | - | ❌ No |
| Limit | - | Unlimited |

### 2.4 Reserved Default
- **SiloID = "default org UUID"**
- Assigned to all existing and new organizations
- Used when siloId is not provided

---

## 3. Functional Requirements

### 3.1 Silo Configuration

**Behavior:**
- Admin defines silos in config UI
- No deletion allowed
- Allow renaming of the Silo
- Will need to have a SiloID (GUID or UUID) and a Silo Name (Name will be visible in the UI)

**Acceptance Criteria:**
- ✅ Admin can create Silo
- ✅ Silo persists across system
- ✅ System prevents duplicate Silo IDs per org
- ✅ System prevents delete operation

---

### 3.2 Cookie Consent

**Behavior:**
- Each cookie banner → exactly one silo
- Many banners → same silo allowed

**Storage:**
```
Consent = Org + ConsumerKey + SiloID
```

**API Example - Create Cookie Banner:**
```json
POST /cookie/banner

{
  "orgId": "123",
  "name": "Arena Banner",
  "siloId": "UUID"
}
```

**Acceptance Criteria:**
- ✅ Banner must have valid siloId
- ✅ Consent reads/writes must include silo filtering
- ✅ Banner can change siloId

---

### 3.3 Preferences System

**Behavior:**
Each Silo contains:
- Independent preference schema
- Independent integration credentials (e.g., Klaviyo)

**API Example - Set Preferences:**
```json
POST /preferences

{
  "orgId": "123",
  "consumerKey": "user@email.com",
  "siloId": "UUID",
  "preferences": {
    "email_marketing": true,
    "sms_marketing": false
  }
}
```

**API Example - Get Preferences:**
```
GET /preferences?orgId=123&consumerKey=user@email.com&siloId=UUID
```

**Acceptance Criteria:**
- ✅ Preferences must be silo-scoped
- ✅ Same consumer can have multiple distinct records
- ✅ Preference schema must be silo-specific
- ✅ Integration credentials resolved by silo

---

### 3.4 Brand System

**Behavior:**

| Mapping | Rule |
|---------|------|
| Brand → Silo | 1:1 |
| Silo → Brand | 1:N |

**API Example:**
```json
POST /brand

{
  "name": "Phoenix Suns",
  "siloId": "UUID"
}
```

**Acceptance Criteria:**
- ✅ Brand must have valid silo
- ✅ Brand siloId can change
- ✅ Changing silo does NOT retroactively change stored data

---

### 3.5 Consumer Relationship System

**Behavior:**
- Consumer records do not have silo identifiers
- Consumers that log in to a specific branded portal only see the preferences and data privacy requests of the silo for the specified brand
- Consumers that log in to the Parent Organization's consumer portal would see all data privacy requests across all brands and would have to select a brand before editing preferences

---

### 3.6 Data Privacy Requests

**Behavior:**

Silo assignment priority:
1. Brand
2. Default "org"

**API Example:**
```json
POST /privacy/request

{
  "orgId": "123",
  "consumerKey": "user@email.com",
  "brandId": "brand_1"
}
```

→ System resolves: `"siloId": "UUID"`

**Acceptance Criteria:**
- ✅ Every request must have siloId
- ✅ Silo determined at time of creation
- ❌ Silo cannot be changed after creation
- ✅ Audit logs must include siloId

---

### 3.7 Permissions (Users & Groups)

**Behavior:**

Users have either:
```json
{
  "allowedSilos": ["UUID", "UUID2"]
}
```

OR:
```json
{
  "isAdmin": true
}
```

**Rules:**

| Condition | Behavior |
|-----------|----------|
| No silo access | No visibility |
| Brand assigned | Silo access granted |
| Admin | Full access |

**Acceptance Criteria:**
- ✅ Silo filtering enforced at query level
- ✅ Admin bypass works consistently
- ✅ Brand assignment auto-adds silo
- ✅ Users with access to 1 brand that shares a silo with other brands should still only have access to the 1 brand
- ✅ Removing brand removes silo access

---

## 4. API Contract (Global Rules)

### 4.1 Silo Field
```json
"siloId": "UUID"
```

**Rules:**

| Case | Behavior |
|------|----------|
| Missing siloId | Default to default org UUID |
| Invalid siloId | Reject request |
| Admin request | May ignore filtering |

**Validation Example:**
```json
{
  "error": "INVALID_SILO_ID",
  "message": "Silo ID not found for organization"
}
```

---

## 5. Database Design

### Required Changes

Add silo_id column to:
- preferences
- consent
- requests
- brands
- cookie_configs

### Indexing
```sql
CREATE INDEX idx_consumer_silo 
ON consumer_data (org_id, consumer_key, silo_id);
```

### Create Table
```sql
CREATE TABLE silos 
…
```

### Query Example
```sql
SELECT * FROM preferences
WHERE org_id = ?
AND consumer_key = ?
AND silo_id = ?;
```

---

## 6. Security Enforcement

**Silo filtering MUST occur at:**
- ✅ Database Layer (Required)
- ✅ API Layer
- ✅ UI Layer

**Critical Rule:**
> No data should EVER be returned across silos unless user is admin

---

## 7. UI Requirements

### Config UI
- Silo Management screen
- Add new silos
- Cannot delete silos
- Assign silos to:
  - Brands
  - Cookies
  - Preferences

### Operational UI
- Add silo selector
- Filter:
  - Preferences
  - Privacy requests
  - Consent data

---

## 8. Migration Strategy

### Existing Data
```
Assign siloId = "default org UUID"
```

**Acceptance Criteria:**
- ✅ Zero downtime migration
- ✅ No data loss
- ✅ Legacy APIs continue working

---

## 9. Edge Cases & Validation

**Case 1: Missing siloId**
→ Default to "default org UUID"

**Case 2: Entity changes silo**
→ New data uses new silo
→ Old data remains unchanged

**Case 3: User loses silo access**
→ Data becomes invisible

**Case 4: Admin access**
→ Ignore silo filters

---

## 10. Acceptance Criteria (System Level)

### Data Isolation
- ✅ Consumer has separate data across silos
- ✅ No cross-silo visibility

### Performance
- ✅ Queries remain performant with composite index
- ✅ No full table scans introduced

### Security
- ✅ Silo enforced at DB level
- ✅ Unauthorized access blocked

### Compatibility
- ✅ Existing clients operate unchanged
- ✅ No required API updates

---

## 11. Implementation Notes (Engineering)

- Treat siloId as mandatory internal key
- Always resolve default early in request pipeline
- Avoid nullable silo fields in DB
- Inject silo filtering in API layer (not UI)
