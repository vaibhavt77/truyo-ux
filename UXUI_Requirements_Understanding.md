# Truyo Silo Extension - UX/UI Requirements Understanding

**Project:** Truyo Silo Extension  
**Role:** Lead UX/UI Designer  
**Product Owner:** Rod  
**Date:** June 29, 2026  
**Status:** Requirements Understanding Phase

---

## Executive Summary

This document outlines the UX/UI aspects of the Truyo Silo Extension feature. It identifies all UI-related components that need design, clarifies user flows, and documents key questions to be addressed in the detailed requirements meeting with the Product Owner.

---

## Section 1: UI Components Identified from PRD

### 1.1 Admin Configuration Interface

#### 1.1.1 Silo Management Screen
- **Purpose:** Allow admins to create, view, and manage silos
- **Key Features:**
  - Create new silos (with SiloID and Silo Name)
  - View all silos for the organization
  - Rename silos
  - ❌ Delete operation NOT allowed (must be disabled/hidden)
  - Display silo IDs (UUID/GUID)

#### 1.1.2 Silo Assignment Interface
- **Purpose:** Assign silos to various entities
- **Assignment Targets:**
  - Brands
  - Cookie configurations
  - Preferences

#### 1.1.3 Brand Management with Silo Assignment
- **Purpose:** Manage brands and their silo associations
- **Key Features:**
  - Create/edit brands
  - Assign/change silo for a brand
  - Display Brand ↔ Silo mapping (1:1 Brand → Silo, 1:N Silo → Brand)
  - Show which brands share the same silo

#### 1.1.4 Cookie Configuration with Silo Assignment
- **Purpose:** Configure cookie banners with silo context
- **Key Features:**
  - Create/edit cookie banners
  - Assign/change silo for banner
  - Show banner name and associated silo
  - Display which silos have multiple banners

#### 1.1.5 Permissions Management UI
- **Purpose:** Manage user and group permissions for silo access
- **Key Features:**
  - Assign users/groups to specific silos
  - Define allowedSilos list for users
  - Mark users as admin (full access)
  - Display current permissions
  - Show silo access by user/group

---

### 1.2 Operational Interface (End-User/Operator)

#### 1.2.1 Silo Selector Component
- **Purpose:** Allow users to filter data by silo
- **Usage Context:**
  - Preferences view
  - Privacy requests view
  - Consent data view
- **Behavior:**
  - Dropdown or selection component
  - Display only silos the user has access to
  - Support switching between silos
  - Indicate current silo selection

#### 1.2.2 Preferences Management Screen
- **Purpose:** Display and manage consumer preferences scoped to silo
- **Key Features:**
  - Show silo context (selected silo)
  - Display preferences for current silo only
  - Allow editing preferences within silo context
  - Show silo-specific integration credentials (e.g., Klaviyo)
  - For parent org users: display all brands with ability to select before editing

#### 1.2.3 Privacy Requests View
- **Purpose:** Display data privacy requests scoped to silo
- **Key Features:**
  - Show silo context
  - Filter privacy requests by silo
  - Display silo information for each request
  - Show request status, creation time, and silo assignment
  - For parent org users: allow filtering by brand

#### 1.2.4 Consent Data Management
- **Purpose:** Display and manage consent records scoped to silo
- **Key Features:**
  - Show silo context
  - Filter consent data by silo
  - Display cookie banner associations
  - Show consent status by silo
  - Display when consent was recorded

---

### 1.3 Consumer Portal Variations

#### 1.3.1 Brand-Specific Portal
- **Purpose:** Consumers access brand-specific data
- **User Flow:**
  - Consumer logs in → automatically sees only their silo's data
  - No explicit silo selector needed (implicit by brand context)
  - See only:
    - Preferences for this brand's silo
    - Privacy requests for this brand's silo
    - Consent data for this brand's silo

#### 1.3.2 Parent Organization Portal
- **Purpose:** Consumers see all their data across all brands
- **User Flow:**
  - Consumer logs in → sees all brands they have data with
  - See all privacy requests across all brands
  - Must select a brand BEFORE editing preferences
  - Silo selector may be implicit (tied to brand selection)
  - Options:
    - Show silo information or keep it hidden from consumer?

---

## Section 2: User Flows Requiring UI Design

### 2.1 Admin Flow: Create and Manage Silos

**Flow Steps:**
1. Admin navigates to Silo Management
2. Admin clicks "Create New Silo"
3. Modal/form appears requesting:
   - Silo Name (text input)
   - SiloID auto-generated or manual input?
4. Admin submits → Silo created
5. Admin can rename existing silo
6. Admin cannot delete (button disabled)
7. Admin sees list of all silos with option to assign to brands/cookies/preferences

**Questions:**
- Should SiloID be auto-generated or user-entered?
- How many silos per org typically? (affects list UI complexity)

---

### 2.2 Admin Flow: Assign Silo to Brand

**Flow Steps:**
1. Admin navigates to Brand Management
2. Admin creates new brand or edits existing
3. Admin selects silo from dropdown
4. Admin saves brand
5. Silo is assigned (1:1 mapping displayed)
6. Later: Admin can change silo for brand (old data unchanged)

**Questions:**
- Should changing a silo for a brand show a warning about old data?
- How should "silo is already assigned to another brand" be handled?
- Should there be bulk brand assignment to a silo?

---

### 2.3 Operator Flow: Manage Consumer Preferences (Brand Portal)

**Flow Steps:**
1. Operator logs into brand-specific portal
2. Operator sees consumer preferences automatically filtered to this silo
3. Operator selects a consumer
4. Operator views/edits preferences for the silo
5. Silo context shown in header/breadcrumb

**Questions:**
- Should the silo name be visible in the UI or kept hidden?
- Should operators see that a consumer has data in other silos?

---

### 2.4 Operator Flow: Manage Consumer Preferences (Parent Org Portal)

**Flow Steps:**
1. Operator logs into parent org portal
2. Operator sees all brands and associated data
3. Operator selects a consumer
4. System shows all privacy requests across all brands
5. To edit preferences: Operator must select a brand first
6. After selecting brand → Preferences for that silo shown
7. Silo selection implicit or explicit?

**Questions:**
- How should the brand selection UI work? (dropdown, modal, multi-select?)
- Should the silo be explicitly shown or remain backend-only?
- Should operator see "Consumer has 3 brands" indicator?

---

### 2.5 Operator Flow: View Consent Data with Silo Filtering

**Flow Steps:**
1. Operator navigates to Consent Management
2. Operator selects silo from dropdown (if permission-based access)
3. Operator sees all consent records for the silo
4. Consent records grouped by banner/brand
5. Operator can filter by banner, date, silo

**Questions:**
- What's the default silo selection when page loads?
- Should silo selector be always visible or only if user has multi-silo access?
- How to organize consent data with multiple silos? (tabs, sections, separate views?)

---

### 2.6 User Flow: View Privacy Requests with Silo Filtering

**Flow Steps:**
1. User navigates to Privacy Requests
2. User sees all privacy requests across silos they have access to
3. Each request shows associated silo/brand
4. User can filter by silo, brand, status, date
5. User can take action on request (delete, export data, etc.)

**Questions:**
- Should privacy requests be grouped by silo?
- How prominently should silo information be displayed?
- For multi-silo users, what's the default view? (all silos or first silo?)

---

### 2.7 Permission Flow: Grant Silo Access to User

**Flow Steps:**
1. Admin navigates to User Management
2. Admin selects or creates a user
3. Admin sees permission assignment section
4. Admin either:
   - Assigns specific silos: `allowedSilos: ["UUID1", "UUID2"]`
   - OR marks as admin: `isAdmin: true`
5. Admin assigns brand to user (auto-grants silo access)
6. User with partial access sees only their silos
7. Admin sees all silos

**Questions:**
- How to visually distinguish between silo-specific and admin users?
- Should there be a "select all silos" option or explicit list only?
- When assigning brand to user, should silo be shown or hidden?

---

## Section 3: Critical UX/UI Questions for Detailed Meeting

### **3.1 Silo Selector/Filter Component**

1. **Visibility & Placement:**
   - Should the silo selector be always visible in the UI or context-dependent?
   - Where should it appear? (top-left, top-center, sidebar, page header?)
   - Should different features have silo selector in different locations?

2. **For Brand-Specific Portals:**
   - Should silo selector be hidden (implicit by brand)?
   - Or should it display the silo name for transparency?

3. **For Parent Org Portals:**
   - Should silo selection be explicit (dropdown) or implicit (tied to brand)?
   - Should users see both "Brand" and "Silo" selectors or just "Brand"?

4. **Interaction Behavior:**
   - When switching silos, should the page:
     - Reload? (full page refresh)
     - Filter dynamically? (AJAX-based)
     - Show a transition/loading state?
   - Should there be an "apply filter" button or auto-apply on selection?

5. **Multi-Silo Users:**
   - If user has access to 2 brands sharing the same silo, should they see the silo is "shared"?
   - Should there be a "show all my silos" option?

---

### **3.2 Default Silo Handling**

1. **Default Silo Display:**
   - Should "default org UUID" silo be visible to users or hidden?
   - Should it be labeled as "Default" or by org name?
   - Should it behave differently from custom silos?

2. **Default Behavior:**
   - When a user first loads the app, which silo should be selected?
   - Should the app remember their last selected silo?
   - For new users, should there be a silo selection flow?

---

### **3.3 Silo Information & Transparency**

1. **Transparency to Different User Types:**
   - **Admin users:** Should always see silo IDs and names?
   - **Operators:** Should see silo names, IDs, or neither?
   - **Consumers (brand portal):** Should see any silo information?
   - **Consumers (parent org portal):** Should see silo names?

2. **Silo Context Display:**
   - Should silo context be shown in:
     - Page headers? (e.g., "Preferences for [SiloName]")
     - Breadcrumbs? (e.g., "Admin > Silos > [SiloName] > Preferences")
     - Table columns? (display silo name for each row)
     - Badges/pills next to data?

3. **Multiple Silos in Lists:**
   - If viewing data from multiple silos (e.g., "all privacy requests across silos"):
     - Should each row show the silo?
     - Should data be grouped by silo in sections?
     - Should there be color coding by silo?
     - Should silo information be in a tooltip/hover state?

---

### **3.4 Consumer Portal Flows**

1. **Brand-Specific Portal:**
   - Should the consumer see the brand name, silo name, or both?
   - Should there be any indication that their data is "siloed"?
   - If a consumer has the same email in multiple silos (brands), should they see all in one login?

2. **Parent Org Portal:**
   - How should brand selection work?
     - Dropdown on page load?
     - Modal before accessing preferences?
     - Expandable list/accordion?
     - Separate "Brand Hub" page first?

3. **Displaying Data Across Brands:**
   - For privacy requests across brands:
     - Should each request show the brand name?
     - Should requests be grouped by brand?
     - Should there be a "select brand" filter?

---

### **3.5 Permission Assignment UX**

1. **User Permission UI:**
   - How should "allowedSilos" be visually represented?
     - Checkboxes for each silo?
     - Multi-select dropdown?
     - Pill/tag selector?
   - Should users see silo IDs or just names?

2. **Brand-Based Permission:**
   - When assigning a brand to a user, should silo be:
     - Auto-populated in background (user unaware)?
     - Shown for transparency?
     - Part of a separate silo permission step?

3. **Admin Indicator:**
   - Should admin users see a visual badge/indicator?
   - Should there be a way to see which users are admins?

---

### **3.6 Error & Validation Messages**

1. **Invalid Silo Access:**
   - If user tries to access a silo they don't have permission for, what should happen?
     - Error message?
     - Redirect to allowed silo?
     - Show empty state?

2. **Missing Silo ID:**
   - Should users see the error "INVALID_SILO_ID"?
   - Or should this be handled silently (default to default org UUID)?

3. **Silo Changes:**
   - If a brand's silo changes, should there be a notification/warning?
   - Should users be informed that old data remains in old silo?

---

### **3.7 Search & Discoverability**

1. **Searching Across Silos:**
   - If user searches for a consumer, should:
     - Results be filtered to their current silo only?
     - Results show all silos with silo badge?
     - Search be silo-specific or global?

2. **Silo Filter in Lists:**
   - Should preferences/privacy requests/consent have:
     - A separate silo filter column?
     - A silo filter in the filter bar?
     - Ability to sort/group by silo?

---

### **3.8 Mobile & Responsive Considerations**

1. **Silo Selector on Mobile:**
   - Should silo selector be visible on mobile?
   - If yes, how? (top bar dropdown, bottom sheet, etc.)
   - Should it be collapsible?

2. **Multi-Silo Data Lists:**
   - On mobile, how should silo information be displayed in lists?
     - Separate column (may not fit)?
     - In row expand/details view?
     - As a badge?

---

### **3.9 Visual Design & Patterns**

1. **Silo Identification:**
   - Should silos have:
     - Color coding?
     - Icons?
     - Visual indicators?
   - If multiple silos appear in same view, should each have distinct styling?

2. **Consistency:**
   - Should silo selectors look the same across all pages?
   - Should the same component be used for all filtering?

3. **Empty States:**
   - What should user see if:
     - They have no silo access? (error, message, or redirect?)
     - No data exists for selected silo?
     - Only default silo is available?

---

### **3.10 Accessibility & Compliance**

1. **Screen Reader Support:**
   - How should silo context be announced?
   - Should silo selector be keyboard accessible?

2. **Color Dependency:**
   - If using color coding for silos, is there text backup?

3. **WCAG Compliance:**
   - Are there specific WCAG levels we need to meet?

---

## Section 4: Design Artifacts Needed

Based on the requirements, the following UI mockups/designs are needed:

### **Admin Interfaces:**
- [ ] Silo Management Dashboard
- [ ] Create/Edit Silo Modal
- [ ] Brand Management with Silo Assignment
- [ ] Cookie Configuration with Silo Assignment
- [ ] User Permission Assignment (silo-based access)

### **Operational Interfaces:**
- [ ] Preferences Management Screen (with silo selector)
- [ ] Privacy Requests View (with silo filtering)
- [ ] Consent Data Management (with silo filtering)

### **Consumer Portals:**
- [ ] Brand-Specific Portal (implicit silo)
- [ ] Parent Org Portal (multi-brand, brand selection flow)

### **Components:**
- [ ] Silo Selector/Dropdown Component
- [ ] Silo Badge/Indicator
- [ ] Silo Filter Bar
- [ ] Permission Assignment Component

### **States & Edge Cases:**
- [ ] Error state: Invalid silo access
- [ ] Empty state: No data for silo
- [ ] Loading state: Switching silos
- [ ] Multi-silo user interface

---

## Section 5: Key Design Constraints & Notes

1. **No Delete Operation:** Silos cannot be deleted - UI must enforce/indicate this
2. **Immutable Silo Assignment:** Data's silo cannot be changed after creation (only applies to new data)
3. **Default Silo:** Must exist and be transparent to system (may be transparent to users too)
4. **Backward Compatibility:** Existing clients should work unchanged (consider legacy UI updates)
5. **Security:** Silo filtering must be consistent across UI, API, and DB layers
6. **Permission-Based Visibility:** Users only see data for silos they have access to

---

## Next Steps

1. Schedule detailed requirements meeting with Rod (Product Owner)
2. Present these questions and get clarifications
3. Create detailed wireframes/mockups based on responses
4. Design system component definitions
5. Create interaction specifications and flows
6. Prepare accessibility audit plan
7. Create design specs document with all answers integrated

---

**Document Status:** Ready for Discussion  
**Last Updated:** June 29, 2026
**Author:** Vaibhav Tarale
