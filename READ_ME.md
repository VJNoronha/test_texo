Conversation opened. 2 messages. 2 messages unread.

Skip to content
Using Gmail with screen readers
1 of 8,385
(no subject)
Inbox

NIVED KRISHNA
9:37 AM (15 minutes ago)
to me

https://texo-backoffice-966597289997.europe-west1.run.app/

NIVED KRISHNA
Attachments
9:45 AM (6 minutes ago)
to me



On Mon, Feb 9, 2026 at 9:36 AM NIVED KRISHNA <nithupd@gmail.com> wrote:
https://texo-backoffice-966597289997.europe-west1.run.app/
 One attachment
  •  Scanned by Gmail
# TEXO Platform - End-to-End QA Test Plan

**Document Version:** 1.0  
**Date:** February 9, 2026  
**Tester Name:** _________________________  
**Test Environment:** UAT  
**Platform URL:** _________________________

---

## 📋 Table of Contents
1. [Introduction](#introduction)
2. [Test Scope](#test-scope)
3. [Test Environment Setup](#test-environment-setup)
4. [Test Credentials](#test-credentials)
5. [Test Cases](#test-cases)
6. [Bug Reporting Template](#bug-reporting-template)
7. [Test Summary Report](#test-summary-report)

---

## 1. Introduction

### 1.1 Purpose
This document provides comprehensive test cases for the TEXO Platform. The platform is a multi-tenant OCR (Optical Character Recognition) management system with credit-based billing.

### 1.2 Platform Overview
**TEXO Platform** allows:
- **Super Admins** to manage tenants, credit plans, and system configuration
- **Tenant Admins** to create applications, manage document types, and process OCR requests
- **ERP Integration** for automated tenant provisioning and credit top-ups

### 1.3 Key Features to Test
- Authentication & User Management
- Tenant Management (Super Admin)
- Credit Plan Management
- Application & API Key Management
- OCR Document Type Configuration
- Credit Balance & Transactions
- Billing & Top-Up Integration
- Dashboard Analytics
- ERP API Integration
- Webhooks Configuration
- Security & Access Control

---

## 2. Test Scope

### 2.1 In Scope
✅ All UI functionality  
✅ API endpoints (via UI interactions)  
✅ User roles and permissions  
✅ Credit system (allocation, consumption, alerts)  
✅ Data validation and error handling  
✅ Cross-browser compatibility (Chrome, Firefox, Safari)  
✅ Responsive design (Desktop, Tablet)

### 2.2 Out of Scope
❌ Performance/Load testing  
❌ Security penetration testing  
❌ Mobile app testing (if not available)  
❌ Direct database testing  
❌ Source code review

---

## 3. Test Environment Setup

### 3.1 Platform Access
- **Frontend URL:** [To be provided]
- **Environment:** UAT (Test Environment)
- **Browser Requirements:** Chrome 120+, Firefox 120+, Safari 17+
- **Screen Resolution:** 1920x1080 (primary), 1366x768 (secondary)

### 3.2 Test Prerequisites
Before starting testing, ensure you have:
- [ ] Access to the platform URL
- [ ] Test credentials (provided below)
- [ ] Sample test images for OCR (driver's license, vehicle registration)
- [ ] Access to email for verification tests
- [ ] API testing tool (Postman/Insomnia) - optional but recommended
- [ ] Note-taking tool for bug documentation

---

## 4. Test Credentials

### 4.1 Super Admin Account
```
Email: admin@texo.com
Password: Admin123!
Role: Super Admin (Full Platform Access)
```

### 4.2 Test Tenant Account
```
Email: test@texo.com
Password: test123
Role: Tenant Admin
Company: Test Company
Initial Credits: 1000
```

### 4.3 Additional Test Data
**ERP API Key:** [To be created during testing]  
**Application API Key:** [To be generated during testing]  
**Sample Webhook URL:** https://webhook.site (create your own unique URL)

---

## 5. Test Cases

---

## MODULE 1: AUTHENTICATION & SESSION MANAGEMENT

### TC-001: Super Admin Login - Valid Credentials
**Priority:** High | **Type:** Functional

**Pre-conditions:**
- Platform URL is accessible
- Super admin account exists

**Test Steps:**
1. Open the platform URL in browser
2. Verify login page loads correctly
3. Enter email: `admin@texo.com`
4. Enter password: `Admin123!`
5. Click "Login" button
6. Observe the page loaded after login

**Expected Results:**
- ✅ Login page displays with email and password fields
- ✅ Login successful without errors
- ✅ Redirected to Super Admin Dashboard
- ✅ Top navigation bar shows "Super Admin" badge or indicator
- ✅ Left sidebar menu shows: Dashboard, Credit Plans, Tenants, ERP API Keys, Webhooks, System Config
- ✅ User profile dropdown visible in top-right corner

**Test Data:**
- Email: admin@texo.com
- Password: Admin123!

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Actual Result:** _________________________  
**Comments:** _________________________

---

### TC-002: Tenant Admin Login - Valid Credentials
**Priority:** High | **Type:** Functional

**Test Steps:**
1. If logged in as super admin, logout first
2. Navigate to login page
3. Enter email: `test@texo.com`
4. Enter password: `test123`
5. Click "Login" button

**Expected Results:**
- ✅ Login successful
- ✅ Redirected to Tenant Dashboard (different from super admin)
- ✅ Can see company name "Test Company" displayed
- ✅ Credit balance widget visible showing "1000" credits
- ✅ Sidebar menu shows: Dashboard, Applications, Document Types, Users, Billing
- ✅ Does NOT show super admin menus (Credit Plans, Tenants, ERP API Keys)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Actual Result:** _________________________

---

### TC-003: Login with Invalid Credentials
**Priority:** High | **Type:** Negative Testing

**Test Steps:**
1. Navigate to login page
2. Enter email: `invalid@test.com`
3. Enter password: `wrongpassword`
4. Click "Login" button

**Expected Results:**
- ✅ Login fails
- ✅ Error message displayed: "User not found" or "Incorrect password"
- ✅ User remains on login page
- ✅ Password field is cleared
- ✅ No redirection occurs

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-004: Logout Functionality
**Priority:** High | **Type:** Functional

**Pre-conditions:** User is logged in (any role)

**Test Steps:**
1. Click on user profile dropdown (top-right corner)
2. Click "Logout" option
3. Verify redirection

**Expected Results:**
- ✅ User logged out successfully
- ✅ Redirected to login page
- ✅ Cannot access protected pages by manually entering URLs
- ✅ Browser back button does not return to authenticated pages
- ✅ Session token cleared (can verify in browser DevTools > Application > Storage)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-005: Session Expiration
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. Login with any valid credentials
2. Wait for 30 minutes without any activity
3. Try to perform any action (e.g., navigate to another page)

**Expected Results:**
- ✅ Session expires after 30 minutes
- ✅ User automatically redirected to login page
- ✅ Message displayed: "Session expired. Please login again."

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 2: SUPER ADMIN - DASHBOARD & ANALYTICS

### TC-006: Super Admin Dashboard - View Statistics
**Priority:** High | **Type:** Functional

**Pre-conditions:** Logged in as super admin

**Test Steps:**
1. After login, observe the dashboard
2. Check all statistics widgets
3. Note down all displayed numbers

**Expected Results:**
Dashboard displays the following widgets:
- ✅ **Total Tenants** - Shows count with active/inactive breakdown
- ✅ **Active Tenants** - Shows number of active tenants
- ✅ **Total Credit Balance** - Sum of all tenant credits
- ✅ **Credits Consumed Today** - Today's consumption across platform
- ✅ **Credits Consumed This Month** - Monthly consumption
- ✅ **Active API Keys** - Count of active ERP API keys
- ✅ **Top Consumers** - Chart/table showing top 10 credit-consuming tenants
- ✅ **Recent Alerts** - List of recent low-credit alerts (if any)
- ✅ All numbers are accurate and load without errors

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Notes:** Record actual numbers seen: _________________________

---

## MODULE 3: SUPER ADMIN - CREDIT PLANS MANAGEMENT

### TC-007: View All Credit Plans
**Priority:** High | **Type:** Functional

**Pre-conditions:** Logged in as super admin

**Test Steps:**
1. Click "Credit Plans" in left sidebar
2. Verify the page loads
3. Count the number of default plans displayed

**Expected Results:**
Page displays a table/list with at least 4 default plans:

| Plan Code | Plan Name | Credits | Price | Status |
|-----------|-----------|---------|-------|--------|
| BASIC | Basic Plan | 1,000 | $50 | Active |
| STANDARD | Standard Plan | 5,000 | $200 | Active |
| PREMIUM | Premium Plan | 20,000 | $700 | Active |
| ENTERPRISE | Enterprise Plan | 100,000 | $3,000 | Active |

- ✅ All 4 plans visible
- ✅ Each plan shows: Code, Name, Credits, Price, Currency (USD), Status
- ✅ Plans are marked as "Active"
- ✅ Can see created date/time for each plan
- ✅ Create Plan button visible at top

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-008: Create Custom Credit Plan
**Priority:** High | **Type:** Functional

**Test Steps:**
1. On Credit Plans page, click "Create Plan" button
2. Fill in the form:
   - Plan Code: `CUSTOM500`
   - Plan Name: `Custom 500 Credits`
   - Default Credits: `500`
   - Price: `25`
   - Currency: `USD` (or default)
   - Description: `Small custom plan for testing`
3. Click "Save" or "Create" button
4. Verify plan appears in the list

**Expected Results:**
- ✅ Form opens with all fields
- ✅ All fields accept input correctly
- ✅ Plan created successfully
- ✅ Success message displayed: "Plan created successfully"
- ✅ New plan appears in the plans list
- ✅ Plan has status "Active"
- ✅ Plan can be selected when creating/updating tenants

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-009: Edit Existing Credit Plan
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. Select the "CUSTOM500" plan created in TC-008
2. Click "Edit" or click on the plan
3. Change Price from `25` to `30`
4. Update Description to `Updated custom plan`
5. Click "Save"

**Expected Results:**
- ✅ Edit form opens with current values pre-filled
- ✅ Can modify price and description
- ✅ Plan updated successfully
- ✅ Success message displayed
- ✅ Changes reflected in the list immediately
- ✅ Audit log created (if audit feature exists)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-010: Deactivate Credit Plan
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. Select the "CUSTOM500" plan
2. Click "Deactivate" or toggle status to inactive
3. Confirm the action if prompted
4. Verify plan status changed

**Expected Results:**
- ✅ Confirmation dialog appears
- ✅ After confirmation, plan status changes to "Inactive"
- ✅ Inactive plan shown with different styling (grayed out or marked)
- ✅ Inactive plan cannot be assigned to new tenants
- ✅ Existing tenants with this plan are NOT affected
- ✅ Can reactivate the plan later

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 4: SUPER ADMIN - TENANT MANAGEMENT

### TC-011: View All Tenants
**Priority:** High | **Type:** Functional

**Pre-conditions:** Logged in as super admin

**Test Steps:**
1. Click "Tenants" in left sidebar
2. Verify tenants list page loads
3. Check columns and data displayed

**Expected Results:**
- ✅ Tenants page displays a table with columns:
  - Tenant ID (TEN-XXXXXXXX format)
  - Company Name
  - Email
  - Credit Plan
  - Credit Balance
  - Status (Active/Inactive)
  - Created Date
- ✅ At least 1 tenant visible ("Test Company")
- ✅ Search/filter functionality available
- ✅ Can sort by columns (click column headers)
- ✅ "Create Tenant" button visible at top
- ✅ Can click on tenant to view details

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Total Tenants Visible:** _________________________

---

### TC-012: Create New Tenant
**Priority:** Critical | **Type:** Functional

**Test Steps:**
1. On Tenants page, click "Create Tenant" button
2. Fill in the form:
   - Company Name: `Alpha Corporation`
   - Email: `admin@alphacorp.com`
   - Phone: `+1234567890`
   - Credit Plan: Select `STANDARD`
3. Click "Create" or "Save" button
4. Wait for confirmation
5. Check if tenant appears in list

**Expected Results:**
- ✅ Form opens with all required fields
- ✅ Email field validates email format
- ✅ Phone field accepts various formats
- ✅ Credit Plan dropdown shows all active plans
- ✅ Tenant created successfully
- ✅ Success message: "Tenant created successfully"
- ✅ New tenant appears in tenants list with:
  - Generated Tenant ID (TEN-XXXXXXXX)
  - Status: Active
  - Credit Balance: 5000 (STANDARD plan default)
- ✅ Admin user auto-created with email `admin@alphacorp.com`
- ✅ Welcome email sent (if email feature enabled)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Generated Tenant ID:** _________________________

---

### TC-013: View Tenant Details
**Priority:** High | **Type:** Functional

**Test Steps:**
1. From tenants list, click on "Alpha Corporation" created in TC-012
2. Verify details page opens
3. Review all displayed information

**Expected Results:**
Details page shows complete tenant information:
- ✅ **Company Info Section:**
  - Company Name: Alpha Corporation
  - Email: admin@alphacorp.com
  - Phone: +1234567890
  - Tenant ID: TEN-XXXXXXXX
  - Status: Active
  - Created Date & Time
  
- ✅ **Credit Information:**
  - Current Plan: STANDARD
  - Total Credits: 5000
  - Used Credits: 0
  - Remaining: 5000
  - Usage: 0%
  
- ✅ **Activity Section (may be empty if just created):**
  - Total Applications: 0
  - Total OCR Requests: 0
  - Recent Transactions
  
- ✅ **Actions Available:**
  - Edit button
  - Deactivate/Activate button
  - View Audit Log button

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-014: Update Tenant Information
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. On tenant details page for "Alpha Corporation"
2. Click "Edit" button
3. Change Phone to: `+9876543210`
4. Change Credit Plan to: `PREMIUM`
5. Click "Save"

**Expected Results:**
- ✅ Edit form opens with current values
- ✅ Can modify phone and plan
- ✅ When plan changed, shows confirmation about credit adjustment
- ✅ Update successful with success message
- ✅ Phone number updated to new value
- ✅ Plan changed to PREMIUM
- ✅ Credit balance adjusted to 20,000 (PREMIUM default)
- ✅ Transaction created for plan change
- ✅ Changes reflected immediately

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-015: Deactivate Tenant
**Priority:** High | **Type:** Functional

**Test Steps:**
1. On tenant details page for "Alpha Corporation"
2. Click "Deactivate" button
3. Confirm the action in dialog
4. Verify status changed

**Expected Results:**
- ✅ Confirmation dialog appears with warning message
- ✅ After confirmation, tenant status changes to "Inactive"
- ✅ Tenant marked inactive in tenants list
- ✅ Tenant admin cannot login (Test by logging out and trying to login with admin@alphacorp.com)
- ✅ Any API keys for this tenant stop working
- ✅ Can reactivate tenant later

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-016: Reactivate Deactivated Tenant
**Priority:** Medium | **Type:** Functional

**Pre-conditions:** Tenant "Alpha Corporation" is deactivated (from TC-015)

**Test Steps:**
1. Go to tenant details for "Alpha Corporation"
2. Click "Activate" button
3. Confirm action
4. Test login with tenant credentials

**Expected Results:**
- ✅ Tenant status changes to "Active"
- ✅ Success message displayed
- ✅ Tenant can now login successfully
- ✅ API keys work again
- ✅ Credit balance preserved from before deactivation

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-017: Search and Filter Tenants
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. Go to Tenants list page
2. Use search box to search for "Alpha"
3. Verify filtering works
4. Clear search and try filter by Status: "Active"
5. Try filter by Plan: "STANDARD"

**Expected Results:**
- ✅ Search by company name works correctly
- ✅ Only matching tenants displayed
- ✅ Filter by status works (Active/Inactive)
- ✅ Filter by plan works
- ✅ Can combine multiple filters
- ✅ "Clear filters" button resets all filters
- ✅ Results update in real-time as you type

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 5: TENANT ADMIN - DASHBOARD

### TC-018: Tenant Dashboard View
**Priority:** High | **Type:** Functional

**Pre-conditions:** 
- Logout from super admin
- Login as tenant: test@texo.com / test123

**Test Steps:**
1. After login, observe the tenant dashboard
2. Review all widgets and sections
3. Note down all statistics

**Expected Results:**
Dashboard displays:

- ✅ **Credit Balance Widget** (Top/Center):
  - Total Credits: 1000
  - Used Credits: 0 (or actual if OCR done)
  - Remaining: 1000
  - Usage meter/progress bar with color:
    - Green if > 50%
    - Yellow if 20-50%
    - Red if < 20%
  - "Top-Up Now" button visible
  
- ✅ **Applications Widget:**
  - Total Applications: Shows count
  - "Create Application" button
  
- ✅ **OCR Requests Widget:**
  - Total Requests (Last 7 days)
  - Success Rate %
  - Average Processing Time
  
- ✅ **Usage Chart:**
  - Line/bar chart showing OCR usage over time
  - Last 7 days data
  
- ✅ **Recent Transactions:**
  - List of recent credit transactions
  - Shows type, amount, date
  
- ✅ **Quick Actions:**
  - Create New Application
  - Create Document Type
  - View Billing

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 6: TENANT ADMIN - APPLICATIONS MANAGEMENT

### TC-019: View Applications List
**Priority:** High | **Type:** Functional

**Pre-conditions:** Logged in as tenant admin

**Test Steps:**
1. Click "Applications" in left sidebar
2. View applications list page

**Expected Results:**
- ✅ Applications page displays correctly
- ✅ Shows table/grid with columns:
  - Application Name
  - Application ID
  - API Key (masked: ••••XXXX)
  - Status (Active/Inactive)
  - Created Date
  - Actions (View, Edit, Delete)
- ✅ "Create Application" button at top
- ✅ If no applications exist, shows empty state with message
- ✅ Can search/filter applications

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-020: Create New Application
**Priority:** Critical | **Type:** Functional

**Test Steps:**
1. On Applications page, click "Create Application"
2. Fill in the form:
   - Application Name: `Invoice Scanner`
   - Description: `Application for scanning and extracting invoice data`
3. Click "Create" button
4. Wait for success message

**Expected Results:**
- ✅ Form opens with name and description fields
- ✅ Name field is required (try submitting empty)
- ✅ Application created successfully
- ✅ Success message: "Application created successfully"
- ✅ Application appears in list with:
  - Generated Application ID (unique ID)
  - Status: Active
  - Auto-generated API Key (64-character hex string)
- ✅ API Key shown in full (shown only once)
- ✅ "Copy API Key" button available
- ✅ Warning message: "Save this API key securely. You won't be able to see it again."

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Generated API Key:** _________________________ (SAVE THIS FOR LATER TESTS)

---

### TC-021: View Application Details
**Priority:** High | **Type:** Functional

**Test Steps:**
1. Click on "Invoice Scanner" application from list
2. View details page

**Expected Results:**
Details page shows:

- ✅ **Basic Information:**
  - Application Name: Invoice Scanner
  - Application ID
  - Description
  - Status: Active
  - Created Date
  
- ✅ **API Key Section:**
  - API Key: Masked (••••last4chars)
  - "Show API Key" button (clicking shows full key temporarily)
  - "Copy API Key" button
  - "Regenerate API Key" button with warning
  
- ✅ **Statistics:**
  - Total OCR Requests: 0 (or actual count)
  - Success Rate: 100% (or actual)
  - Failed Requests: 0
  - Credits Consumed: 0
  
- ✅ **Recent Activity:**
  - List of recent OCR requests (if any)
  - Pagination if > 20 records
  
- ✅ **Actions Available:**
  - Edit Application
  - Deactivate Application
  - Delete Application
  - View Logs

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-022: Regenerate API Key
**Priority:** High | **Type:** Functional

**Test Steps:**
1. On application details page
2. Click "Regenerate API Key" button
3. Read the warning message
4. Confirm action
5. Save the new API key

**Expected Results:**
- ✅ Warning dialog appears: "This will invalidate the old API key. All requests using the old key will fail. Continue?"
- ✅ After confirmation, new API key generated
- ✅ New key shown in full (64-character hex)
- ✅ "Copy" button available
- ✅ Old API key immediately invalidated
- ✅ Success message displayed
- ✅ Audit log created (if audit feature exists)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**New API Key:** _________________________ (UPDATE THIS)

---

### TC-023: Edit Application Details
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. On application details page
2. Click "Edit" button
3. Change Description to: `Updated - Invoice scanning with advanced data extraction`
4. Click "Save"

**Expected Results:**
- ✅ Edit form opens with current values
- ✅ Can modify name and description
- ✅ Cannot change Application ID (read-only)
- ✅ Changes saved successfully
- ✅ Success message displayed
- ✅ Changes reflected immediately on details page

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-024: View Application Logs/Activity
**Priority:** High | **Type:** Functional

**Test Steps:**
1. On application details page
2. Click "Logs" or "Activity" tab/button
3. View the logs page

**Expected Results:**
- ✅ Logs page opens showing OCR request logs
- ✅ Table with columns:
  - Timestamp (Date & Time)
  - Document Type
  - Status (Success/Failed)
  - Credits Consumed
  - Processing Time (ms)
  - Error Message (if failed)
  - Request ID
- ✅ Can filter by:
  - Status (All/Success/Failed)
  - Date Range
  - Document Type
- ✅ Can search by Request ID
- ✅ Pagination works (20 records per page)
- ✅ Can click on log entry to see full details
- ✅ If no logs yet, shows empty state message

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-025: Deactivate Application
**Priority:** High | **Type:** Functional

**Test Steps:**
1. Create another test application: `Test App for Deactivation`
2. Go to its details page
3. Click "Deactivate" button
4. Confirm action

**Expected Results:**
- ✅ Confirmation dialog with warning
- ✅ Application status changes to "Inactive"
- ✅ API key immediately stops working (returns 401 if used)
- ✅ Application shown with "Inactive" badge in list
- ✅ Can filter to show only active/inactive apps
- ✅ Can reactivate later
- ✅ Existing logs preserved

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 7: TENANT ADMIN - DOCUMENT TYPES

### TC-026: View Document Types
**Priority:** High | **Type:** Functional

**Pre-conditions:** Logged in as tenant admin

**Test Steps:**
1. Click "Document Types" in sidebar
2. View the document types list

**Expected Results:**
- ✅ Document Types page displays
- ✅ Shows at least 2 default document types:
  - `drivers_license` - Driver's License
  - `vehicle_registration` - Vehicle Registration
- ✅ Each document type shows:
  - Document Type Code
  - Display Name
  - Number of Fields
  - Status (Active/Inactive)
  - Created Date
- ✅ "Create Document Type" button visible
- ✅ Can click on document type to view/edit schema

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-027: View Document Type Schema
**Priority:** High | **Type:** Functional

**Test Steps:**
1. Click on "drivers_license" document type
2. View schema details

**Expected Results:**
Schema page shows:

- ✅ **Basic Info:**
  - Document Type: drivers_license
  - Display Name: Driver's License
  - Status: Active
  
- ✅ **Field Schema Table:**
  | Field Name | Data Type | Required | Description |
  |------------|-----------|----------|-------------|
  | full_name | string | Yes | Complete name on license |
  | date_of_birth | date | Yes | Birth date (DD/MM/YYYY) |
  | id_number | string | Yes | License number |
  | nationality | string | No | Citizenship |
  | issued_country | string | No | Issuing country |
  | expiry_date | date | No | Expiration date |
  
- ✅ **Extraction Rules:**
  - Descriptions for each field on how to extract data
  
- ✅ **Actions:**
  - Edit Schema button
  - Add Field button
  - Delete Document Type button

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-028: Create Custom Document Type
**Priority:** Critical | **Type:** Functional

**Test Steps:**
1. On Document Types page, click "Create Document Type"
2. Fill Basic Information:
   - Document Type Code: `invoice`
   - Display Name: `Invoice`
   - Description: `Commercial invoice document`
3. Add Fields:
   - **Field 1:**
     - Name: `invoice_number`
     - Type: `string`
     - Required: Yes
     - Extraction Rule: `Extract invoice number from top of document`
   - **Field 2:**
     - Name: `invoice_date`
     - Type: `date`
     - Required: Yes
     - Extraction Rule: `Find invoice date (DD/MM/YYYY or MM/DD/YYYY)`
   - **Field 3:**
     - Name: `total_amount`
     - Type: `currency`
     - Required: Yes
     - Extraction Rule: `Extract total amount including currency symbol`
   - **Field 4:**
     - Name: `vendor_name`
     - Type: `string`
     - Required: No
     - Extraction Rule: `Find vendor/supplier name at top`
4. Click "Create" button

**Expected Results:**
- ✅ Form provides field type options: string, number, date, boolean, email, phone, currency
- ✅ Can add multiple fields
- ✅ Can reorder fields (drag and drop or up/down buttons)
- ✅ Required/Optional toggle works
- ✅ Can add extraction rules for each field
- ✅ Document type created successfully
- ✅ Success message displayed
- ✅ New document type appears in list
- ✅ Can be used for OCR processing immediately

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-029: Edit Document Type Schema
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. Click on "invoice" document type created in TC-028
2. Click "Edit" button
3. Add a new field:
   - Name: `payment_terms`
   - Type: `string`
   - Required: No
   - Extraction Rule: `Find payment terms (e.g., Net 30)`
4. Click "Save"

**Expected Results:**
- ✅ Edit form opens with existing fields
- ✅ Can add new fields
- ✅ Can modify existing fields
- ✅ Can delete fields (with confirmation)
- ✅ Cannot change document type code (read-only)
- ✅ Changes saved successfully
- ✅ New field available for OCR extraction
- ✅ Existing OCR logs not affected (backward compatible)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-030: Delete/Deactivate Document Type
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. Create a new document type: `test_document`
2. Go to its details page
3. Click "Delete" or "Deactivate" button
4. Confirm action

**Expected Results:**
- ✅ Warning dialog appears
- ✅ If document type has been used in OCR requests, shows warning message
- ✅ Document type marked inactive or deleted
- ✅ No longer appears in active document types list
- ✅ Cannot be used for new OCR requests
- ✅ Existing OCR logs preserved
- ✅ Can view in "Show Inactive" filter

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 8: CREDIT MANAGEMENT & BILLING

### TC-031: View Credit Balance
**Priority:** High | **Type:** Functional

**Pre-conditions:** Logged in as tenant admin

**Test Steps:**
1. View dashboard credit widget
2. Navigate to Billing page for detailed view

**Expected Results:**
- ✅ **Dashboard Widget Shows:**
  - Total Purchased: 1000
  - Consumed: 0 (or actual)
  - Remaining: 1000
  - Usage: 0%
  - Progress bar with appropriate color
  
- ✅ **Billing Page Shows:**
  - Current Plan: BASIC
  - Credit Details breakdown
  - "Top-Up Now" button prominent
  - Transaction history tab
  - Alert settings tab

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Actual Balance Seen:** _________________________

---

### TC-032: View Transaction History
**Priority:** High | **Type:** Functional

**Test Steps:**
1. Go to Billing page
2. Click "Transaction History" tab
3. Review transactions

**Expected Results:**
- ✅ Transactions table displays with columns:
  - Transaction ID (TXN-YYYYMMDD-XXXXXXXX)
  - Type (Purchase/Consumption/Adjustment/Refund)
  - Credits (+ or -)
  - Balance Before
  - Balance After
  - Date & Time
  - Description
  - Reference ID
- ✅ At least 1 transaction visible: Initial credit allocation
- ✅ Can filter by:
  - Transaction Type
  - Date Range
- ✅ Can search by Transaction ID
- ✅ Pagination works
- ✅ Can export transactions (CSV/PDF) if feature exists

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-033: Top-Up Credits - Odoo Redirect
**Priority:** Critical | **Type:** Functional

**Pre-conditions:** 
- Odoo URL must be configured by super admin (coordinate with super admin to set this up first)

**Test Steps:**
1. On Billing page, click "Top-Up Now" button
2. Observe what happens

**Expected Results:**
- ✅ Button click triggers redirect
- ✅ Redirected to Odoo portal URL: `https://{odoo-url}/saas/auto_login?token=XXXXX`
- ✅ Token is present in URL
- ✅ Token is valid JWT format
- ✅ Auto-login to Odoo portal works (if Odoo is configured and running)
- ✅ User sees their tenant information in Odoo
- ✅ Can purchase credits in Odoo (if integrated)

**Note:** If Odoo is not set up, this test will fail. Document if backend returns error message or if redirect fails.

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Error/Issue:** _________________________

---

### TC-034: Credit Consumption via OCR
**Priority:** Critical | **Type:** Functional

**Pre-conditions:** 
- Have valid API key from TC-020
- Have sample image file

**Test Steps:**
1. Note current credit balance
2. Use API tool (Postman) or wait for API test section
3. Make 1 OCR request
4. Return to Billing page
5. Check balance updated

**Expected Results:**
- ✅ After successful OCR request:
  - Credit balance reduced by 1
  - New transaction created:
    - Type: Consumption
    - Credits: -1
    - Balance updated correctly
  - Transaction appears in history
  - Dashboard meter updated

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Balance Before:** _____ | **Balance After:** _____

---

### TC-035: Configure Credit Alerts
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. Go to Billing page
2. Click "Alert Settings" tab
3. Configure thresholds:
   - Enable alerts
   - Set threshold: 20% (200 credits for 1000 total)
   - Alert email: [your test email]
4. Click "Save"

**Expected Results:**
- ✅ Alert configuration form available
- ✅ Can set multiple threshold levels: 20%, 10%, 5%
- ✅ Email field validates email format
- ✅ Enable/disable toggle works
- ✅ Settings saved successfully
- ✅ Success message displayed
- ✅ Alert will trigger when balance reaches threshold

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-036: Low Credit Alert Trigger (Manual)
**Priority:** Medium | **Type:** Functional

**Pre-conditions:** 
- Alert configured in TC-035
- Need to consume credits to reach threshold

**Test Steps:**
1. Make multiple OCR requests to consume credits
2. Monitor balance until it drops below 200 (20% of 1000)
3. Check dashboard for alerts
4. Check email for alert notification

**Expected Results:**
- ✅ When balance < 20%:
  - Dashboard shows red/warning banner
  - Alert message: "⚠️ Low Credit Balance: Only X credits remaining"
  - Email notification sent to configured email
  - Email subject: "⚠️ Low Credit Balance Alert - Test Company"
  - Email contains:
    - Current balance
    - Threshold triggered
    - Link to top-up
    - Tenant name
- ✅ Alert recorded in alerts table/database
- ✅ Super admin can see alerts in their dashboard

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 9: OCR API INTEGRATION

**Note:** These tests require API testing tool like Postman. If you don't have access to make API calls, coordinate with developer to provide you with a test interface or skip this module.

### TC-037: API Health Check
**Priority:** High | **Type:** API Testing

**Test Steps:**
1. Open Postman or API testing tool
2. Send GET request to: `{API_URL}/api/v2/health`

**Expected Results:**
- ✅ Status Code: 200 OK
- ✅ Response body:
```json
{
  "status": "healthy",
  "timestamp": "2026-02-09T10:30:00Z"
}
```

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-038: OCR Request - Valid Driver's License
**Priority:** Critical | **Type:** API Testing

**Pre-conditions:**
- Have API key from TC-020
- Have sample driver's license image (JPEG/PNG)

**API Request:**
```
POST {API_URL}/api/v2/ocr/process
Headers:
  X-API-Key: [Your API Key from TC-020]
  Content-Type: multipart/form-data
Body (form-data):
  image: [Upload driver's license image file]
  document_type: drivers_license
```

**Expected Results:**
- ✅ Status Code: 200 OK
- ✅ Response body contains:
```json
{
  "request_id": "UUID",
  "document_type": "drivers_license",
  "status": "success",
  "extracted_data": {
    "full_name": "John Doe",
    "date_of_birth": "1990-01-15",
    "id_number": "DL123456789",
    "nationality": "US",
    "issued_country": "USA",
    "expiry_date": "2028-01-15"
  },
  "confidence_score": 0.95,
  "processing_time_ms": 2500,
  "credits_consumed": 1
}
```
- ✅ Credits deducted from balance
- ✅ Request logged in application logs
- ✅ Processing time < 5 seconds

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Request ID:** _________________________

---

### TC-039: OCR Request - Invalid API Key
**Priority:** High | **Type:** Negative Testing

**API Request:**
```
POST {API_URL}/api/v2/ocr/process
Headers:
  X-API-Key: invalid_api_key_123456
  Content-Type: multipart/form-data
Body:
  image: [any image]
  document_type: drivers_license
```

**Expected Results:**
- ✅ Status Code: 401 Unauthorized
- ✅ Response body:
```json
{
  "error": "Invalid API key",
  "message": "The provided API key is invalid or has been revoked"
}
```
- ✅ No credits consumed
- ✅ Request not processed

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-040: OCR Request - Insufficient Credits
**Priority:** High | **Type:** Negative Testing

**Pre-conditions:** 
- Tenant has 0 credits (consume all credits or ask super admin to set balance to 0)

**API Request:** Same as TC-038 with valid API key

**Expected Results:**
- ✅ Status Code: 402 Payment Required
- ✅ Response body:
```json
{
  "error": "Insufficient credits",
  "message": "Your account has insufficient credits to process this request",
  "current_balance": 0,
  "credits_required": 1
}
```
- ✅ Request not processed
- ✅ No credits deducted (already 0)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-041: OCR Request - Invalid Document Type
**Priority:** Medium | **Type:** Negative Testing

**API Request:**
```
POST {API_URL}/api/v2/ocr/process
Headers:
  X-API-Key: [Valid API Key]
  Content-Type: multipart/form-data
Body:
  image: [any image]
  document_type: nonexistent_type
```

**Expected Results:**
- ✅ Status Code: 400 Bad Request
- ✅ Response body:
```json
{
  "error": "Invalid document type",
  "message": "Document type 'nonexistent_type' not found",
  "available_types": ["drivers_license", "vehicle_registration", "invoice"]
}
```
- ✅ No credits consumed

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-042: OCR Request - Invalid Image Format
**Priority:** Medium | **Type:** Negative Testing

**API Request:**
```
POST {API_URL}/api/v2/ocr/process
Headers:
  X-API-Key: [Valid API Key]
  Content-Type: multipart/form-data
Body:
  image: [Upload .txt or .pdf file instead of image]
  document_type: drivers_license
```

**Expected Results:**
- ✅ Status Code: 400 Bad Request
- ✅ Response body:
```json
{
  "error": "Invalid image format",
  "message": "Only JPEG and PNG images are supported",
  "received_format": "text/plain"
}
```
- ✅ No credits consumed

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-043: OCR Request - Image Size Limit
**Priority:** Medium | **Type:** Negative Testing

**API Request:**
```
POST {API_URL}/api/v2/ocr/process
Headers:
  X-API-Key: [Valid API Key]
  Content-Type: multipart/form-data
Body:
  image: [Upload image > 10MB]
  document_type: drivers_license
```

**Expected Results:**
- ✅ Status Code: 413 Payload Too Large
- ✅ Response body:
```json
{
  "error": "Image too large",
  "message": "Maximum image size is 10MB",
  "received_size_mb": 15.5,
  "max_size_mb": 10
}
```
- ✅ No credits consumed

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-044: OCR Request - Missing Required Fields
**Priority:** Medium | **Type:** Negative Testing

**API Request:**
```
POST {API_URL}/api/v2/ocr/process
Headers:
  X-API-Key: [Valid API Key]
  Content-Type: multipart/form-data
Body:
  document_type: drivers_license
  [No image file attached]
```

**Expected Results:**
- ✅ Status Code: 400 Bad Request
- ✅ Response body:
```json
{
  "error": "Missing required field",
  "message": "Image file is required",
  "required_fields": ["image", "document_type"]
}
```

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-045: OCR Request - Custom Document Type (Invoice)
**Priority:** High | **Type:** Functional

**Pre-conditions:** 
- Invoice document type created in TC-028
- Have sample invoice image

**API Request:**
```
POST {API_URL}/api/v2/ocr/process
Headers:
  X-API-Key: [Valid API Key]
  Content-Type: multipart/form-data
Body:
  image: [Upload invoice image]
  document_type: invoice
```

**Expected Results:**
- ✅ Status Code: 200 OK
- ✅ Response contains extracted fields matching schema:
```json
{
  "extracted_data": {
    "invoice_number": "INV-2026-001",
    "invoice_date": "2026-02-01",
    "total_amount": "1250.00 USD",
    "vendor_name": "ABC Company",
    "payment_terms": "Net 30"
  },
  "credits_consumed": 1
}
```
- ✅ All custom fields extracted
- ✅ Credits deducted

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 10: SUPER ADMIN - ERP API KEYS

### TC-046: View ERP API Keys
**Priority:** High | **Type:** Functional

**Pre-conditions:** Logged in as super admin

**Test Steps:**
1. Click "ERP API Keys" in sidebar
2. View ERP API keys page

**Expected Results:**
- ✅ ERP API Keys page displays
- ✅ Table shows columns:
  - Key Name
  - Key ID (key_XXXXXXXX)
  - Status (Active/Revoked)
  - Created Date
  - Last Used (timestamp)
  - Created By
- ✅ "Create API Key" button at top
- ✅ Can filter by status
- ✅ Can search by name

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-047: Create ERP API Key
**Priority:** Critical | **Type:** Functional

**Test Steps:**
1. Click "Create API Key" button
2. Fill in form:
   - Key Name: `Kiyzer.ai Production`
   - Description: `Production integration key for Kiyzer.ai ERP`
3. Click "Generate" button

**Expected Results:**
- ✅ Form opens with name and description fields
- ✅ After clicking Generate:
  - API key generated (64-character hex string)
  - Key displayed in full (one-time only)
  - "Copy API Key" button available
  - Warning message: "Save this key now. You won't be able to see it again."
- ✅ Key ID created (key_XXXXXXXX format)
- ✅ Key appears in list with status: Active
- ✅ Can be used immediately for ERP API calls

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Generated ERP API Key:** _________________________ (**SAVE THIS**)

---

### TC-048: Revoke ERP API Key
**Priority:** High | **Type:** Functional

**Test Steps:**
1. Create another test ERP API key: `Test Key`
2. Click on the test key
3. Click "Revoke" button
4. Confirm action

**Expected Results:**
- ✅ Confirmation dialog appears
- ✅ After confirmation, key status changes to "Revoked"
- ✅ Revoked key cannot be used for API calls (returns 401)
- ✅ Key shown with "Revoked" badge
- ✅ Cannot unrevokeonce revoked (permanent)
- ✅ Audit log created

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-049: ERP API - Create Tenant via API
**Priority:** Critical | **Type:** API Testing

**Pre-conditions:** Have ERP API key from TC-047

**API Request:**
```
POST {API_URL}/api/erp/tenants/create
Headers:
  X-API-Key: [ERP API Key from TC-047]
  Content-Type: application/json
Body:
{
  "company_name": "Beta Industries",
  "email": "admin@betaindustries.com",
  "phone": "+1555123456",
  "plan_code": "PREMIUM"
}
```

**Expected Results:**
- ✅ Status Code: 201 Created
- ✅ Response body:
```json
{
  "success": true,
  "tenant_id": "TEN-XXXXXXXX",
  "message": "Tenant created successfully",
  "admin_user": {
    "email": "admin@betaindustries.com",
    "temporary_password": "RandomPass123!"
  },
  "credit_balance": {
    "plan": "PREMIUM",
    "credits_allocated": 20000
  }
}
```
- ✅ Tenant appears in super admin tenants list
- ✅ Admin user can login with credentials
- ✅ Credits allocated correctly (20,000 for PREMIUM)
- ✅ Welcome email sent (if configured)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Created Tenant ID:** _________________________  
**Admin Password:** _________________________

---

### TC-050: ERP API - Add Credits to Tenant
**Priority:** Critical | **Type:** API Testing

**Pre-conditions:** 
- Have ERP API key
- Have existing tenant ID (use Test Company or Beta Industries)

**API Request:**
```
POST {API_URL}/api/erp/credits/add
Headers:
  X-API-Key: [ERP API Key]
  Content-Type: application/json
Body:
{
  "tenant_id": "TEN-XXXXXXXX",
  "credits": 5000,
  "reference_id": "ODOO-ORDER-12345",
  "description": "Credit purchase via Odoo"
}
```

**Expected Results:**
- ✅ Status Code: 200 OK
- ✅ Response body:
```json
{
  "success": true,
  "transaction_id": "TXN-20260209-XXXXXXXX",
  "balance_before": 1000,
  "balance_after": 6000,
  "credits_added": 5000,
  "current_balance": 6000
}
```
- ✅ Credits added to tenant balance
- ✅ Transaction created in database
- ✅ Transaction visible in tenant's billing history
- ✅ Dashboard updated immediately

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-051: ERP API - Get Tenant Usage Stats
**Priority:** Medium | **Type:** API Testing

**API Request:**
```
GET {API_URL}/api/erp/tenants/{tenant_id}/usage
Headers:
  X-API-Key: [ERP API Key]
```

**Expected Results:**
- ✅ Status Code: 200 OK
- ✅ Response body:
```json
{
  "tenant_id": "TEN-XXXXXXXX",
  "company_name": "Test Company",
  "current_balance": 6000,
  "total_credits_purchased": 6000,
  "total_credits_consumed": 0,
  "total_ocr_requests": 0,
  "total_applications": 1,
  "plan": "BASIC",
  "status": "active"
}
```
- ✅ All data accurate
- ✅ Real-time data

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 11: SUPER ADMIN - WEBHOOKS

### TC-052: View Webhook Configuration
**Priority:** Medium | **Type:** Functional

**Pre-conditions:** Logged in as super admin

**Test Steps:**
1. Click "Webhooks" in sidebar
2. View webhook configuration page

**Expected Results:**
- ✅ Webhook configuration page displays
- ✅ Form shows:
  - Webhook URL field
  - Enable/Disable toggle
  - Event checkboxes:
    - ☐ tenant_created
    - ☐ credit_low_alert
    - ☐ credit_exhausted
    - ☐ credit_purchased
    - ☐ application_created
  - Secret key (auto-generated, read-only)
  - Test Webhook button
- ✅ Current configuration displayed (if already set)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-053: Configure Webhook
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. Go to https://webhook.site and get your unique URL
2. On Webhooks page, enter:
   - Webhook URL: [Your webhook.site URL]
   - Enable: Yes
   - Select events: tenant_created, credit_low_alert
3. Click "Test Webhook" button
4. Click "Save"

**Expected Results:**
- ✅ URL validation (must be HTTPS)
- ✅ Test webhook sends POST request
- ✅ Can see test request in webhook.site
- ✅ Test payload contains:
```json
{
  "event": "test",
  "timestamp": "2026-02-09T10:30:00Z",
  "message": "Webhook test successful"
}
```
- ✅ Configuration saved successfully
- ✅ Webhooks will trigger on selected events

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Webhook URL Used:** _________________________

---

### TC-054: Webhook Delivery - Tenant Created Event
**Priority:** Medium | **Type:** Functional

**Pre-conditions:** Webhook configured in TC-053

**Test Steps:**
1. Keep webhook.site open in another tab
2. Create a new tenant via super admin (or ERP API)
3. Check webhook.site for incoming request

**Expected Results:**
- ✅ Webhook POST request received within 5 seconds
- ✅ Request headers contain:
  - Content-Type: application/json
  - X-Webhook-Signature: [HMAC signature]
  - X-Event-Type: tenant_created
- ✅ Payload contains:
```json
{
  "event": "tenant_created",
  "timestamp": "2026-02-09T10:30:00Z",
  "data": {
    "tenant_id": "TEN-XXXXXXXX",
    "company_name": "...",
    "email": "...",
    "plan": "...",
    "credits_allocated": 1000
  }
}
```
- ✅ Signature can be verified using secret key

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-055: Webhook Delivery - Credit Low Alert Event
**Priority:** Medium | **Type:** Functional

**Pre-conditions:** 
- Webhook configured for credit_low_alert event
- Have tenant with low credit threshold set

**Test Steps:**
1. Consume credits until balance drops below threshold
2. Check webhook.site for alert

**Expected Results:**
- ✅ Webhook triggered when threshold reached
- ✅ Payload contains:
```json
{
  "event": "credit_low_alert",
  "timestamp": "...",
  "data": {
    "tenant_id": "TEN-XXXXXXXX",
    "company_name": "Test Company",
    "current_balance": 150,
    "threshold": 200,
    "threshold_percentage": 20,
    "alert_level": "warning"
  }
}
```

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-056: Disable Webhook
**Priority:** Low | **Type:** Functional

**Test Steps:**
1. Go to Webhooks page
2. Toggle "Enable" to OFF
3. Save configuration
4. Create a test tenant
5. Check webhook.site

**Expected Results:**
- ✅ Webhook disabled successfully
- ✅ No webhooks sent after disabling
- ✅ Configuration preserved (URL and events saved)
- ✅ Can re-enable later

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 12: SUPER ADMIN - SYSTEM CONFIGURATION

### TC-057: View System Configuration
**Priority:** High | **Type:** Functional

**Pre-conditions:** Logged in as super admin

**Test Steps:**
1. Click "System Config" in sidebar
2. View configuration page

**Expected Results:**
- ✅ System Config page displays
- ✅ Shows sections:
  - **Odoo Integration:**
    - Odoo URL field
    - Current URL displayed (if set)
    - Edit button
  - **JWT Configuration (Info only):**
    - JWT secret (not displayed, just info it exists)
    - Token expiry: 10 minutes
  - **Integration Flow (Documentation):**
    - How top-up redirect works
    - Token structure info
- ✅ Can edit Odoo URL

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-058: Configure Odoo URL
**Priority:** Critical | **Type:** Functional

**Test Steps:**
1. Click "Edit" on Odoo Integration section
2. Enter Odoo URL: `https://demo.odoo.com`
3. Click "Save"

**Expected Results:**
- ✅ URL field validates format (must start with https://)
- ✅ Invalid URLs rejected (e.g., http://, malformed)
- ✅ Configuration saved successfully
- ✅ Success message displayed
- ✅ All tenants will now use this URL for top-up
- ✅ Can test by clicking tenant "Top-Up Now" button
- ✅ Audit log created

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-059: Update Odoo URL
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. Change Odoo URL to: `https://texo-demo.odoo.com`
2. Save configuration
3. Test top-up button from tenant account

**Expected Results:**
- ✅ URL updated successfully
- ✅ New URL used immediately
- ✅ No need to restart services
- ✅ All tenants affected by change

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 13: USER MANAGEMENT (TENANT ADMIN)

### TC-060: View Users List
**Priority:** Medium | **Type:** Functional

**Pre-conditions:** Logged in as tenant admin

**Test Steps:**
1. Click "Users" in sidebar
2. View users list

**Expected Results:**
- ✅ Users page displays
- ✅ Shows table with columns:
  - Name
  - Email
  - Role
  - Status (Active/Inactive)
  - Created Date
- ✅ At least 1 user visible (admin user)
- ✅ "Invite User" or "Create User" button at top
- ✅ Can search users
- ✅ Can filter by role/status

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-061: Create/Invite New User
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. Click "Create User" or "Invite User"
2. Fill in form:
   - Name: `John Smith`
   - Email: `john.smith@testcompany.com`
   - Role: `User` (or available roles)
3. Click "Create" or "Send Invite"

**Expected Results:**
- ✅ Form opens with all fields
- ✅ Role dropdown shows available roles
- ✅ Email validates format
- ✅ User created/invited successfully
- ✅ If invited: Invitation email sent
- ✅ User appears in list
- ✅ User can login (if created with password) or accept invite

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-062: Edit User Details
**Priority:** Low | **Type:** Functional

**Test Steps:**
1. Click on a user from the list
2. Click "Edit"
3. Change user's role or other details
4. Save changes

**Expected Results:**
- ✅ Edit form opens
- ✅ Can modify name, role, status
- ✅ Cannot change email (read-only)
- ✅ Changes saved successfully
- ✅ User's access updated based on new role

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-063: Deactivate User
**Priority:** Medium | **Type:** Functional

**Test Steps:**
1. Select a non-admin user
2. Click "Deactivate"
3. Confirm action
4. Test if user can login

**Expected Results:**
- ✅ User status changed to Inactive
- ✅ User cannot login (gets error message)
- ✅ User's API requests blocked
- ✅ Can reactivate later
- ✅ Admin user cannot be deactivated (validation)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 14: SECURITY & ACCESS CONTROL

### TC-064: Role-Based Access - Super Admin
**Priority:** High | **Type:** Security

**Pre-conditions:** Logged in as super admin

**Test Steps:**
1. Try to access all menu items
2. Try to perform all actions

**Expected Results:**
- ✅ Can access all routes:
  - Dashboard
  - Credit Plans (view, create, edit, delete)
  - Tenants (view, create, edit, deactivate)
  - ERP API Keys (view, create, revoke)
  - Webhooks (configure, test)
  - System Config (view, edit)
- ✅ Can view all tenants' data
- ✅ Can perform all admin actions
- ✅ No 403 Forbidden errors

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-065: Role-Based Access - Tenant Admin
**Priority:** High | **Type:** Security

**Pre-conditions:** Logged in as tenant admin

**Test Steps:**
1. Try to access super admin routes manually
2. Try URLs like:
   - `/super-admin/plans`
   - `/super-admin/tenants`
   - `/super-admin/erp-keys`

**Expected Results:**
- ✅ Cannot access super admin routes
- ✅ 403 Forbidden or redirected to dashboard
- ✅ Left menu does NOT show super admin options
- ✅ Can only access:
  - Dashboard (own data)
  - Applications (own company)
  - Document Types (own company)
  - Users (own company)
  - Billing (own company)
- ✅ Cannot see other tenants' data

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-066: Client Isolation - Data Separation
**Priority:** Critical | **Type:** Security

**Pre-conditions:** 
- Have 2 tenants: Test Company and Beta Industries

**Test Steps:**
1. Login as Test Company admin
2. Note application IDs, credit balance
3. Logout
4. Login as Beta Industries admin
5. Check if any Test Company data visible

**Expected Results:**
- ✅ Each tenant sees ONLY their own:
  - Applications
  - Credit balance
  - Transactions
  - Users
  - OCR logs
  - Document types (custom ones)
- ✅ No way to access other tenant's data
- ✅ Application IDs different
- ✅ Cannot use API key from one tenant in another tenant's requests
- ✅ Complete data isolation

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-067: Password Security
**Priority:** High | **Type:** Security

**Test Steps:**
1. Try to create user with weak password
2. Test password requirements

**Expected Results:**
- ✅ Password must meet requirements:
  - Minimum 8 characters
  - At least 1 uppercase letter
  - At least 1 lowercase letter
  - At least 1 number
  - Optional: Special character
- ✅ Weak passwords rejected with clear error message
- ✅ Strong passwords accepted

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-068: Session Security
**Priority:** High | **Type:** Security

**Test Steps:**
1. Login successfully
2. Open browser DevTools > Application > Storage
3. Check for JWT token in localStorage/sessionStorage
4. Copy token
5. Open incognito window
6. Try to manually set token and access protected route

**Expected Results:**
- ✅ JWT token stored securely
- ✅ Token contains user claims (inspect token at jwt.io)
- ✅ Token has expiry (30 minutes)
- ✅ Cannot reuse token across different browsers/devices (optional based on implementation)
- ✅ Token validated on every request

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 15: UI/UX & CROSS-BROWSER TESTING

### TC-069: Responsive Design - Desktop
**Priority:** Medium | **Type:** UI/UX

**Test Steps:**
1. Test platform on different desktop resolutions:
   - 1920x1080 (Full HD)
   - 1366x768 (Laptop)
   - 2560x1440 (2K)
2. Check all major pages

**Expected Results:**
- ✅ All pages display correctly at all resolutions
- ✅ No horizontal scrolling
- ✅ All buttons and forms accessible
- ✅ Tables responsive (scroll or collapse)
- ✅ Charts and graphs scale properly
- ✅ Navigation menu accessible

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Issues Found:** _________________________

---

### TC-070: Responsive Design - Tablet
**Priority:** Low | **Type:** UI/UX

**Test Steps:**
1. Test on tablet (iPad or similar)
2. Or use browser DevTools responsive mode
3. Set to 768x1024 (portrait) and 1024x768 (landscape)

**Expected Results:**
- ✅ Platform usable on tablet
- ✅ Navigation adapts (hamburger menu if needed)
- ✅ Tables scroll horizontally or stack
- ✅ Forms remain usable
- ✅ Touch targets adequate size

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-071: Browser Compatibility - Chrome
**Priority:** High | **Type:** Compatibility

**Test Steps:**
1. Test all critical features in Chrome (latest version)

**Expected Results:**
- ✅ All features work in Chrome
- ✅ No console errors
- ✅ UI renders correctly
- ✅ No performance issues

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Chrome Version:** _________________________

---

### TC-072: Browser Compatibility - Firefox
**Priority:** High | **Type:** Compatibility

**Test Steps:**
1. Test all critical features in Firefox (latest version)

**Expected Results:**
- ✅ All features work in Firefox
- ✅ No console errors
- ✅ UI renders correctly
- ✅ No performance issues

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Firefox Version:** _________________________

---

### TC-073: Browser Compatibility - Safari (if available)
**Priority:** Medium | **Type:** Compatibility

**Test Steps:**
1. Test all critical features in Safari (latest version)

**Expected Results:**
- ✅ All features work in Safari
- ✅ No console errors
- ✅ UI renders correctly
- ✅ No performance issues

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked  
**Safari Version:** _________________________

---

### TC-074: Form Validation & Error Handling
**Priority:** High | **Type:** UI/UX

**Test Steps:**
1. Try to submit empty forms (login, create tenant, etc.)
2. Enter invalid data (invalid email, etc.)
3. Check error messages

**Expected Results:**
- ✅ Required field validation works
- ✅ Error messages clear and helpful
- ✅ Errors displayed near relevant fields
- ✅ Form doesn't submit with invalid data
- ✅ Success messages clear
- ✅ Error states visually distinct (red borders, icons)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-075: Loading States & Spinners
**Priority:** Medium | **Type:** UI/UX

**Test Steps:**
1. Perform actions that require API calls
2. Observe loading indicators

**Expected Results:**
- ✅ Loading spinners shown during API calls
- ✅ Buttons disabled during submission
- ✅ "Loading..." or similar text displayed
- ✅ User cannot double-submit forms
- ✅ Skeleton loaders for data-heavy pages (optional)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-076: Empty States
**Priority:** Low | **Type:** UI/UX

**Test Steps:**
1. View pages with no data (new tenant, no applications)
2. Check empty state messages

**Expected Results:**
- ✅ Helpful empty state messages displayed
- ✅ Example: "No applications yet. Create your first application to get started."
- ✅ Call-to-action button present
- ✅ Optional: Illustrative icons or graphics

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-077: Navigation & Breadcrumbs
**Priority:** Medium | **Type:** UI/UX

**Test Steps:**
1. Navigate through multiple pages
2. Check if navigation is intuitive
3. Check for breadcrumbs

**Expected Results:**
- ✅ Left sidebar navigation clear and organized
- ✅ Active page highlighted in menu
- ✅ Breadcrumbs show current location (e.g., Home > Tenants > View Tenant)
- ✅ Back button works correctly
- ✅ Logo click returns to dashboard

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-078: Search & Filter Performance
**Priority:** Medium | **Type:** Performance

**Test Steps:**
1. Use search on tenants list
2. Use filters on various pages
3. Note response time

**Expected Results:**
- ✅ Search results appear quickly (< 1 second)
- ✅ Filters apply without page reload
- ✅ Large lists (100+ items) paginate correctly
- ✅ No performance degradation with more data

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 16: DATA INTEGRITY & EDGE CASES

### TC-079: Concurrent Credit Consumption
**Priority:** High | **Type:** Edge Case

**Test Steps:**
1. Have tenant with 10 credits
2. Make 11 OCR requests simultaneously (if possible using API tool)
3. Check final balance

**Expected Results:**
- ✅ 10 requests succeed (consume 10 credits)
- ✅ 1 request fails with "Insufficient credits"
- ✅ Balance exactly 0 (no negative balance)
- ✅ Race condition handled correctly
- ✅ All transactions logged accurately

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-080: Large Transaction History
**Priority:** Low | **Type:** Performance

**Test Steps:**
1. Have tenant with many transactions (100+)
2. View transaction history
3. Test pagination

**Expected Results:**
- ✅ Page loads in reasonable time (< 3 seconds)
- ✅ Pagination works smoothly
- ✅ Can navigate through all pages
- ✅ Search and filter still work
- ✅ No browser freezing

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-081: Special Characters in Input
**Priority:** Medium | **Type:** Edge Case

**Test Steps:**
1. Try creating tenant with special characters:
   - Company: `O'Brien & Sons <Company>`
   - Email: `test+tag@example.com`
2. Try creating application with emojis: `📱 Mobile App`

**Expected Results:**
- ✅ System handles special characters correctly
- ✅ Data saved and retrieved without corruption
- ✅ No SQL injection vulnerabilities
- ✅ No XSS vulnerabilities (HTML tags escaped)

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-082: Maximum Field Lengths
**Priority:** Low | **Type:** Edge Case

**Test Steps:**
1. Try entering very long text in various fields
2. Test limits

**Expected Results:**
- ✅ Fields have reasonable max lengths
- ✅ Error messages if exceeded
- ✅ No UI breaking with long text
- ✅ Text truncation with ellipsis if needed
- ✅ Full text viewable on hover/expansion

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-083: Duplicate Prevention
**Priority:** Medium | **Type:** Data Integrity

**Test Steps:**
1. Try creating tenant with duplicate email
2. Try creating document type with duplicate code
3. Try creating application with duplicate name (if should be unique)

**Expected Results:**
- ✅ System prevents duplicates where appropriate
- ✅ Clear error message: "Email already exists"
- ✅ Suggests existing record or alternative
- ✅ User can proceed with unique value

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-084: Zero Credit Balance Operations
**Priority:** High | **Type:** Edge Case

**Test Steps:**
1. Exhaust all credits (make OCR requests until 0)
2. Try to:
   - Make another OCR request
   - View dashboard
   - View billing page
   - Top-up
3. Add credits back and test platform works normally

**Expected Results:**
- ✅ OCR requests blocked with clear message
- ✅ Dashboard shows "0 credits" with red indicator
- ✅ "Top-Up Now" button prominently displayed
- ✅ All other features still accessible (view apps, logs, etc.)
- ✅ After top-up, platform works normally again

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

## MODULE 17: ERROR RECOVERY & RESILIENCE

### TC-085: Network Timeout Handling
**Priority:** Medium | **Type:** Reliability

**Test Steps:**
1. Open browser DevTools > Network tab
2. Throttle to "Slow 3G" or "Offline"
3. Try to perform actions
4. Restore network

**Expected Results:**
- ✅ Appropriate error messages displayed
- ✅ "Unable to connect to server" or similar
- ✅ Retry button available
- ✅ No data corruption
- ✅ When network restored, can retry and succeed

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-086: Browser Refresh During Operation
**Priority:** Low | **Type:** Reliability

**Test Steps:**
1. Start creating a tenant/application
2. Before clicking save, refresh browser (F5)
3. Check if data lost or saved

**Expected Results:**
- ✅ Unsaved data lost (expected behavior)
- ✅ Or: Warning before refresh: "You have unsaved changes"
- ✅ After refresh, login session persists
- ✅ Can start operation again
- ✅ No partial/corrupted data saved

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

### TC-087: Back Button Behavior
**Priority:** Low | **Type:** UI/UX

**Test Steps:**
1. Navigate: Dashboard → Tenants → View Tenant → Edit Tenant
2. Use browser back button
3. Check navigation flow

**Expected Results:**
- ✅ Back button works correctly
- ✅ Returns to previous page
- ✅ No duplicate entries in history
- ✅ Form data cleared on back (no stale data)
- ✅ No errors when using back button

**Status:** ☐ Pass | ☐ Fail | ☐ Blocked

---

---

## 6. Bug Reporting Template

When you find a bug, document it using this format:

---

**Bug ID:** BUG-001  
**Module:** [e.g., Credit Management]  
**Test Case:** [e.g., TC-034]  
**Severity:** Critical / High / Medium / Low  
**Priority:** P1 / P2 / P3 / P4

**Summary:**  
[One-line description of the bug]

**Steps to Reproduce:**
1. Step 1
2. Step 2
3. Step 3

**Expected Result:**  
[What should happen]

**Actual Result:**  
[What actually happened]

**Screenshots:**  
[Attach screenshots if possible]

**Environment:**
- Browser: Chrome 120.0
- OS: Windows 11 / macOS / Linux
- Screen Resolution: 1920x1080
- User Role: Super Admin / Tenant Admin

**Logs/Error Messages:**  
[Copy any error messages from console or UI]

**Workaround:**  
[If any workaround exists]

**Reproducibility:**  
Always / Sometimes / Rare

**Additional Notes:**  
[Any other relevant information]

---

---

## 7. Test Summary Report

After completing all tests, fill out this summary report:

---

### Test Execution Summary

**Tester Name:** _________________________  
**Test Start Date:** _________________________  
**Test End Date:** _________________________  
**Total Test Duration:** _________ hours

### Overall Statistics

| Metric | Count |
|--------|-------|
| Total Test Cases | 87 |
| Test Cases Executed | ____ |
| Passed | ____ |
| Failed | ____ |
| Blocked | ____ |
| Not Executed | ____ |
| Pass Rate | ____% |

### Module-wise Summary

| Module | Total | Passed | Failed | Blocked | Pass % |
|--------|-------|--------|--------|---------|--------|
| Authentication | 5 | ___ | ___ | ___ | ___% |
| Super Admin - Dashboard | 1 | ___ | ___ | ___ | ___% |
| Credit Plans | 4 | ___ | ___ | ___ | ___% |
| Tenant Management | 7 | ___ | ___ | ___ | ___% |
| Tenant Dashboard | 1 | ___ | ___ | ___ | ___% |
| Applications | 7 | ___ | ___ | ___ | ___% |
| Document Types | 5 | ___ | ___ | ___ | ___% |
| Credit & Billing | 6 | ___ | ___ | ___ | ___% |
| OCR API | 9 | ___ | ___ | ___ | ___% |
| ERP API Keys | 6 | ___ | ___ | ___ | ___% |
| Webhooks | 5 | ___ | ___ | ___ | ___% |
| System Config | 3 | ___ | ___ | ___ | ___% |
| User Management | 4 | ___ | ___ | ___ | ___% |
| Security | 5 | ___ | ___ | ___ | ___% |
| UI/UX | 9 | ___ | ___ | ___ | ___% |
| Data Integrity | 6 | ___ | ___ | ___ | ___% |
| Error Recovery | 3 | ___ | ___ | ___ | ___% |

### Bugs Found

| Severity | Count |
|----------|-------|
| Critical | ___ |
| High | ___ |
| Medium | ___ |
| Low | ___ |
| **Total** | **___** |

### Critical Issues (if any)

1. [BUG-XXX] Brief description - Status: Open/Fixed
2. [BUG-XXX] Brief description - Status: Open/Fixed
3. ...

### Browser Compatibility

| Browser | Version | Status | Issues |
|---------|---------|--------|--------|
| Chrome | _____ | ✅ / ❌ | ___ |
| Firefox | _____ | ✅ / ❌ | ___ |
| Safari | _____ | ✅ / ❌ | ___ |

### Key Findings

**Strengths:**
- [List positive aspects of the platform]
- 
- 

**Issues:**
- [List main problems found]
- 
- 

**Recommendations:**
- [High priority fixes needed]
- [Enhancements suggested]
- [Security concerns]

### Test Environment Details

**Platform URL:** _________________________  
**Environment:** UAT / Staging / Production  
**Tested Features:** All core features ✅

### Sign-off

**Tested By:** _________________________  
**Date:** _________________________  
**Signature:** _________________________

**QA Manager Approval:** _________________________  
**Date:** _________________________

---

## 📌 IMPORTANT NOTES FOR TESTER

1. **Test Systematically:**
   - Follow test cases in order
   - Don't skip pre-conditions
   - Document everything

2. **Take Screenshots:**
   - Capture every bug with screenshot
   - Take screenshots of successful flows for evidence
   - Use annotation tools to highlight issues

3. **Check Console:**
   - Open browser DevTools (F12) during testing
   - Check Console tab for JavaScript errors
   - Check Network tab for failed API calls

4. **Clear Cache Between Tests:**
   - Clear browser cache periodically
   - Use incognito/private mode for fresh tests
   - Test with clean state

5. **Test Both Happy & Negative Paths:**
   - Don't just test expected behavior
   - Try to break the system
   - Test edge cases and invalid inputs

6. **Document Everything:**
   - Even small UI glitches are worth noting
   - Include browser/OS in bug reports
   - Note down any workarounds found

7. **Communicate:**
   - Report critical bugs immediately
   - Don't wait until end of testing
   - Ask questions if test case unclear

8. **Time Management:**
   - Critical features take priority (Auth, Credit System, OCR)
   - If blocked, move to next test case
   - Track time spent per module

---

## 🎯 CRITICAL PATH TESTS (MUST PASS)

If time is limited, focus on these critical tests first:

**Priority 1 (Critical):**
- TC-001, TC-002: Login
- TC-012: Create Tenant
- TC-020: Create Application
- TC-028: Create Document Type
- TC-038: OCR Request (Success)
- TC-047: Create ERP API Key
- TC-049: ERP Create Tenant
- TC-050: ERP Add Credits
- TC-058: Configure Odoo URL

**Priority 2 (High):**
- TC-011: View Tenants
- TC-031-034: Credit Management
- TC-064-066: Security & Access Control

**Priority 3 (Medium):**
- All UI/UX tests
- All error handling tests
- Browser compatibility

---

**END OF TEST PLAN**

*For questions or clarifications, contact the development team.*
QA_TEST_PLAN.md
Displaying QA_TEST_PLAN.md.
