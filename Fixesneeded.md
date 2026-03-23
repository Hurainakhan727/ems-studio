Fix the following 20 issues in the EMS prototype. Read every point carefully and fix ALL of them. Do not skip any. Do not break anything that is already working.

═══════════════════════════════════════════════════════════════
FIX 1 — Remove Export Report button from dashboard
═══════════════════════════════════════════════════════════════

On the main HR/Admin dashboard home page, there is an "Export Report" button in the page header next to "+ Add Employee". Remove it completely. Do not replace it with anything. The "+ Add Employee" button stays.

═══════════════════════════════════════════════════════════════
FIX 2 — Pending Actions buttons must navigate and open relevant content
═══════════════════════════════════════════════════════════════

On the HR/Admin dashboard, the Pending Actions card has action buttons like [Review →], [Mark →], [Fix →]. Right now they do nothing. Fix them:

"3 leave requests awaiting approval" → [Review →]
  Clicking this must navigate to /leave and automatically open the Pending tab
  showing only the pending leave requests

"Attendance incomplete 3 employees" → [Mark →]
  Clicking this must navigate to /attendance and open today's attendance sheet
  with the unmarked employees visually highlighted in amber

"Bank info missing EMP004, EMP005" → [Fix →]
  Clicking this must navigate to /employees and filter/highlight EMP004 and EMP005
  OR open EMP004's edit form directly at the Bank Information step of the wizard

Each button must lead somewhere real and relevant. No dead buttons.

═══════════════════════════════════════════════════════════════
FIX 3 — Search bar must work for HR and Admin roles
═══════════════════════════════════════════════════════════════

The search bar in the topbar (visible to HR and Super Admin) must be fully functional.

When HR or Admin types an employee name or ID (e.g. "Ahmed Ali" or "EMP001"):
  Show a dropdown of results below the search bar as they type (live search)
  Each result row shows: avatar initials + employee name + ID + department
  Clicking a result navigates to /employees/EMP001 (that employee's detail page)
  The employee detail page shows ALL sections: Personal, Job Info, Medical,
  Attendance, Leave, Payslips, Promotions, Penalties

Search should match against: employee name, employee ID, department, designation.
Highlight the matching text in the dropdown results.

For the Employee role: the search bar is hidden entirely. Employees have no use for global search.

═══════════════════════════════════════════════════════════════
FIX 4 — Replace "HR Pro ERP · Real-time Workforce Command Center" with company name
═══════════════════════════════════════════════════════════════

Remove the text "HR Pro ERP · Real-time Workforce Command Center" from the dashboard header subtitle line.

Replace it with:
  "ESSPL · Electronic Safety & Security (Pvt.) Ltd"

Apply this same company name anywhere "HR Pro ERP" appears in the subtitle/description areas of the dashboard. The logo text "HR Pro" in the sidebar can stay as the product name. Only the subtitle description line changes.

═══════════════════════════════════════════════════════════════
FIX 5 — Add Deductions section to the navbar/sidebar
═══════════════════════════════════════════════════════════════

Add a new sidebar link called "Deductions" under the CORE MODULES section, between Leave and Payroll.

Route: /deductions

This page is for HR and Admin only. Employees cannot see it.

PAGE LAYOUT:

Top: "Deductions" page title + [+ Add Deduction] button right

Summary cards (top row):
  Total Deductions This Month | Penalty Deductions | Loan Deductions | Advance Deductions

TABLE:
  Employee | Deduction Type | Amount | Month | Reason | Applied By | Date | Actions
  Actions: edit pencil | delete trash

[+ Add Deduction] button opens a modal:

  Title: "Add Deduction"

  Employee: dropdown (name + ID)
  Month: dropdown (Jan–Dec)
  Year: number input

  Deduction Type: dropdown with these options:
    Penalty — Rule Violation
    Penalty — Dress Code Violation
    Penalty — Eating at Desk
    Penalty — Smoking in Premises
    Penalty — Late Arrival (3+ days)
    Loan Installment
    Advance Recovery
    Other

  When "Penalty — Rule Violation" or similar penalty type is selected:
    Show a sub-section: "Violation Details"
    Checkboxes (multiple can be selected):
      [ ] Drinking in office environment
      [ ] Not wearing office dress code (Male)
      [ ] Not wearing office dress code (Female)
      [ ] Eating at desk
      [ ] Smoking on premises
      [ ] Other (text field for description)

  Amount: PKR input
  Reason / Notes: textarea
  [Cancel] [Apply Deduction]

DECISION BANNER on the page:
"⚠ DECISION NEEDED — Dress Code & Violation Penalties
 Penalty fine amounts for dress code and rule violations have not been decided.
 Options: Fixed fine per violation / Variable amount HR enters each time.
 Please confirm in meeting."

All data saves to localStorage key "ems_deductions".
Added deductions persist after page refresh.

═══════════════════════════════════════════════════════════════
FIX 6 — Employee list page search must highlight matching content
═══════════════════════════════════════════════════════════════

On the /employees page, the search input already exists but may not be working properly.

Fix it so that:
  As HR types in the search box, the employee table filters live (no submit button needed)
  Any text that matches the search query inside the table cells gets highlighted
  Use a yellow background highlight on the matching text (like browser Ctrl+F)
  Matching works on: employee name, employee ID, department, designation, job status
  If no results match: show an empty state "No employees found matching your search"
  Clearing the search box restores the full employee list

═══════════════════════════════════════════════════════════════
FIX 7 — View Payslip button on employee detail page must work
═══════════════════════════════════════════════════════════════

On /employees/EMP001 in the Payslips tab, there is a [View Payslip] button that is not working.

Fix it so that clicking [View Payslip] on any payroll row opens a full payslip modal.

The payslip modal must display exactly this layout (matching the real company payslip format):

┌─────────────────────────────────────────────────────────────┐
│                         PAY SLIP                            │
├────────────────────────────┬────────────────────────────────┤
│ EMPLOYEE DETAILS           │                    Slip # 25   │
├────────────────────────────┤────────────────────────────────┤
│ Employee Code   EMP001     │ Slip No:        25             │
│ Name   Ahmed Ali           │ Dated:  Thu, Mar 31 2026       │
│ Designation Senior Dev     │ Pay Slip for:   March          │
│ Department  Engineering    │ Year:           2026           │
│ DOJ   Jan 15, 2020         │                                │
├────────────────────────────┼────────────────────────────────┤
│ WORKING DAYS               │ SALARY STRUCTURE               │
├────────────────────────────┼────────────────────────────────┤
│ Working Days       31      │ Basic Salary    PKR 1,50,000   │
│ CL                  0      │ House Rent All. PKR   30,000   │
│ ML                  0      │ Medical All.    PKR   10,000   │
│ AL                  0      │ Conveyance      PKR    5,000   │
│ Absents             3      │ Commission      PKR        0   │
│ Total Paid Days    28      │                                │
│                            │ Total           PKR 1,95,000   │
├────────────────────────────┼────────────────────────────────┤
│ EARNINGS                   │ DEDUCTIONS                     │
├────────────────────────────┼────────────────────────────────┤
│ Gross Salary PKR 1,78,666  │ Advance         PKR        0   │
│ Deduction    PKR   3,333   │ Loan            PKR        0   │
│ Net Salary   PKR 1,75,333  │ Absents         PKR    3,333   │
│                            │ Tax             PKR        0   │
│                            │ Late Penalty    PKR        0   │
│                            │ Total           PKR    3,333   │
├────────────────────────────┴────────────────────────────────┤
│ Amount in Words: One lakh seventy five thousand...          │
├──────────────┬──────────────────┬──────────────────────────┤
│ Payment Mode │ Cash [ ]         │ Online Transfer [✓]       │
├──────────────┴──────────────────┴──────────────────────────┤
│  __________________  ____________________  ________________ │
│  Prepare By:         Employee Sign:        Issued By:       │
└─────────────────────────────────────────────────────────────┘

Section header rows (EMPLOYEE DETAILS, WORKING DAYS, SALARY STRUCTURE etc)
must have dark navy background with white text — exactly like a printed form.
All borders visible like a printed table.
Amounts in IBM Plex Mono, right-aligned.

Modal buttons: [Print]  [Download PDF]  [Close]
Print and Download are UI-only (no real functionality needed).

═══════════════════════════════════════════════════════════════
FIX 8 — Remove Deactivate Account button from employee detail page
═══════════════════════════════════════════════════════════════

On /employees/EMP001 (and all employee detail pages), remove the [Deactivate Account] button completely.

This feature has not been decided yet and must not be shown to stakeholders.

Keep: [Edit] button and [Delete Employee] button.
Remove: [Deactivate Account] button only.

═══════════════════════════════════════════════════════════════
FIX 9 — Add Salary section to employee detail page preview
═══════════════════════════════════════════════════════════════

On /employees/EMP001, the tabs currently show: Personal | Job Info | Medical | Attendance | Leave | Payslips | Promotions | Penalties

Add a new tab: "Salary" — insert it between "Job Info" and "Medical"

The Salary tab shows the employee's current salary structure in a clean read-only view:

  Section title: "Current Salary Structure"
  Card with a table:
    Component Name      | Monthly Amount  | Type
    Basic Salary        | PKR 1,50,000   | Earning
    House Rent Allow.   | PKR   30,000   | Earning
    Medical Allowance   | PKR   10,000   | Earning
    Conveyance Allow.   | PKR    5,000   | Earning
    Commission          | PKR        0   | Earning
    ────────────────────────────────────────────
    Total Package       | PKR 1,95,000   | (bold blue)

  Below the table: [Edit Salary] button — clicking opens the salary step of the employee edit wizard

═══════════════════════════════════════════════════════════════
FIX 10 — Department-linked designations in employee add form
═══════════════════════════════════════════════════════════════

On the employee add wizard (/employees/add), in Step 4 — Job Information:

When HR selects a Department from the Department dropdown:
  The Designation dropdown must automatically filter to show only designations
  that belong to the selected department.

If no department is selected yet, the Designation dropdown shows: "Select department first"
If department is changed after designation is already selected, reset the designation field.

Use this department → designation mapping from the dummy data:
  Engineering:  Senior Developer, Junior Developer, Lead Developer, DevOps Engineer
  Marketing:    Marketing Manager, Marketing Executive, Content Writer
  HR:           HR Executive, HR Manager, HR Assistant
  Sales:        Sales Officer, Sales Manager, Sales Executive
  Finance:      Accountant, Finance Manager, Finance Executive

This same filtering must also work on the Designations configuration page
when adding a new designation — show a Department dropdown so every designation
is linked to a department from creation.

═══════════════════════════════════════════════════════════════
FIX 11 — Export buttons on Attendance page: keep UI but add decision banners
═══════════════════════════════════════════════════════════════

On the /attendance page, the [Export Sheet PDF] and [Export Excel] buttons exist.
Do NOT remove them — they look good and stakeholders may want them.

But make them non-functional for now and add a tooltip or small note:
  When hovering over or clicking either export button, show a small popup/toast:
  "Export feature pending stakeholder approval — will be confirmed in meeting"

Also add a yellow DECISION BANNER below the filter row on the attendance page:
"⚠ DECISION NEEDED — Attendance Export
 Should HR be able to export the attendance sheet as PDF and Excel?
 If yes: should it export the current day view, the monthly report, or both?
 Please confirm in meeting."

═══════════════════════════════════════════════════════════════
FIX 12 — Designations must be linked to a Department
═══════════════════════════════════════════════════════════════

On the /settings/designations configuration page:

The table must show an additional column: Department
  Title          | Department   | Actions
  Senior Developer | Engineering | Edit | Delete
  Marketing Manager | Marketing  | Edit | Delete

When adding a new designation via [+ Add] modal:
  Field 1: Designation Title (text input)
  Field 2: Department (dropdown — populated from departments list)
  Both fields are required.

When editing a designation: both Title and Department are editable.

This department link is what powers Fix 10 (filtered designations in employee form).

═══════════════════════════════════════════════════════════════
FIX 13 — Reporting Managers must show their Department
═══════════════════════════════════════════════════════════════

On the /settings/reporting-managers configuration page:

The table must show: Name | Department | Actions

When adding a new reporting manager via [+ Add] modal:
  Field 1: Manager Name (text input)
  Field 2: Department they manage (dropdown)
  Both required.

In the employee add wizard (Step 4 — Job Info), when HR selects a Department,
the Reporting Manager dropdown must filter to show only managers from that department.

═══════════════════════════════════════════════════════════════
FIX 14 — All configuration/settings pages must have working Edit
═══════════════════════════════════════════════════════════════

On ALL of these settings pages, the Edit action must be fully working:
  /settings/departments
  /settings/designations
  /settings/work-modes
  /settings/work-locations
  /settings/employment-types
  /settings/job-statuses
  /settings/reporting-managers
  /settings/shifts
  /settings/leave-types
  /settings/leave-policies
  /settings/payroll-components
  /settings/penalties-config

For each page:
  Clicking the Edit (pencil) icon on any row must open an edit modal
  The modal pre-fills with the current values of that row
  HR saves the changes → the table row updates immediately
  The updated value persists after page refresh (localStorage)

Delete already works — make sure Edit works too. No read-only rows anywhere.

═══════════════════════════════════════════════════════════════
FIX 15 — Add Custom Fields section to sidebar and create the page
═══════════════════════════════════════════════════════════════

Add "Custom Fields" to the sidebar under the ADMINISTRATION section
(visible only to super_admin role).

Route: /settings/custom-fields

PAGE LAYOUT:

Title: "Custom Fields" + subtitle "Manage dynamic form fields across the system"

4 tabs across the top:
  Personal Info | Job Info | Medical Info | Extra Info

Each tab shows a table of custom fields for that section:
  Field Label | Type | Required | Active | Created By | Actions (Edit, Delete)

[+ Add Field] button top right → opens a modal:

  Field Label: text input (e.g. "Passport Number")
  Field Type: dropdown:
    Short Text
    Long Text (textarea)
    Number
    Date
    Dropdown (with options)
    Checkbox (Yes/No)
    File Upload
  Section: dropdown (Personal Info / Job Info / Medical Info / Extra Info)
  Required: toggle (Yes/No)
  Active: toggle (default Yes)

  If "Dropdown" type is selected:
    Show an "Options" section below:
    A list of text inputs for dropdown options
    [+ Add Option] link adds another input row
    Each option row has a [✕] to remove it
    Example: Option 1: "Yes" | Option 2: "No" | Option 3: "Pending"

  [Cancel] [Save Field]

Core fields (name, CNIC, employee ID etc) are shown at the TOP of the Personal Info tab
as read-only rows with a 🔒 lock icon and "Core Field — Cannot be deleted" label.
They cannot be edited or deleted by anyone.

Custom fields appear below the core fields.

DECISION BANNER on the page:
"⚠ DECISION NEEDED — Custom Fields Permissions
 Currently: only super_admin can add/edit/delete custom fields. HR cannot.
 Is this correct? Should HR also be allowed to add custom fields?
 Please confirm in meeting."

All custom field definitions save to localStorage key "ems_custom_fields".

═══════════════════════════════════════════════════════════════
FIX 16 — Add Shifts and Salary Components to configuration sidebar
═══════════════════════════════════════════════════════════════

The following pages must be added to the CONFIGURATION section of the sidebar
if they are not already there:

  Shifts          → /settings/shifts
  Salary Components → /settings/payroll-components

SHIFTS PAGE (/settings/shifts):
  TABLE: Name | Start Time | End Time | Late After (mins) | Active | Actions (Edit, Delete)
  [+ Add Shift] modal: Name, Start Time (24hr), End Time (24hr), Late After Minutes (default 15)
  Edit must pre-fill the modal with existing values.
  All changes persist in localStorage ("ems_shifts").

SALARY COMPONENTS PAGE (/settings/payroll-components):
  TABLE: Component Name | Type (Earning / Deduction) | Taxable | Display Order | Active | Actions
  [+ Add Component] modal:
    Name (text)
    Type: Earning / Deduction (radio)
    Taxable: toggle
    Display Order: number
  Edit pre-fills modal.
  All changes persist in localStorage ("ems_payroll_components").
  Note card at top: "Adding a component here automatically adds it to all payroll generation forms."

═══════════════════════════════════════════════════════════════
FIX 17 — Add Tax Configuration page to configuration section
═══════════════════════════════════════════════════════════════

Add "Tax Config" to the CONFIGURATION section of the sidebar.
Route: /settings/tax-config

PAGE LAYOUT:

Title: "Tax Configuration"
Subtitle: "Define tax brackets applied during payroll generation"

DECISION BANNER at top:
"⚠ DECISION NEEDED — Tax Calculation Method
 Option A: Automatic — system applies tax bracket based on gross salary (shown here)
 Option B: Manual — HR enters tax amount manually each month during payroll generation
 Please confirm in meeting."

TABLE showing tax brackets:
  Salary Range (From) | Salary Range (To) | Tax Rate % | Fixed Amount | Active | Actions
  PKR 0               | PKR 50,000        | 0%         | PKR 0        | Yes    | Edit Delete
  PKR 50,001          | PKR 1,00,000      | 2%         | PKR 0        | Yes    | Edit Delete
  PKR 1,00,001        | PKR 2,00,000      | 5%         | PKR 0        | Yes    | Edit Delete
  PKR 2,00,001        | No limit          | 10%        | PKR 0        | Yes    | Edit Delete

[+ Add Bracket] button → modal:
  From Amount: PKR input
  To Amount: PKR input (or "No limit" checkbox)
  Tax Rate: % input
  Fixed Amount (optional): PKR input (for flat-rate taxes)
  Active: toggle

Edit must pre-fill. Delete shows confirmation.
All brackets persist in localStorage ("ems_tax_config").

Note at bottom: "Tax is calculated automatically during payroll generation
based on the employee's gross salary and the bracket it falls into."

═══════════════════════════════════════════════════════════════
FIX 18 — Employee leave request must appear in admin leave page AND employee dashboard
═══════════════════════════════════════════════════════════════

This is a critical data flow fix. When an employee submits a leave request
from their self-service dashboard (/my-leave or the Apply for Leave modal),
the request must:

1. Save to localStorage key "ems_leave_requests" immediately
2. Appear in the employee's "My Leave Requests" section on their dashboard instantly
3. Appear in the HR/Admin leave management page (/leave) under the Pending tab
4. The pending count badge on the sidebar "Leave" link must update to reflect the new request

For the employee dashboard (/my-dashboard):
  The "My Leave Requests" card must show all requests from localStorage for EMP001
  After applying for leave, the new request appears in the list with status "Pending"
  Leave balance must decrease by the requested days immediately (optimistic update)

For the Apply for Leave modal:
  All fields must work: leave type, from date, to date, days auto-calculated, reason
  Submitting the form saves to localStorage and closes the modal with a success toast
  The leave request list updates immediately without page refresh

═══════════════════════════════════════════════════════════════
FIX 19 — Employee dashboard must default to EMP001 (Ahmed Ali)
═══════════════════════════════════════════════════════════════

When viewing the employee self-service dashboard (/my-dashboard),
always show Ahmed Ali (EMP001) data by default for the demo.

The dashboard must show:
  Welcome: "Welcome back, Ahmed Ali 👋"
  Employee ID: EMP001 | Department: Engineering | Shift: Morning Shift

  Stat cards using EMP001's actual data from localStorage:
    Attendance This Month: 18/22 days (82%)
    Leave Balance: Annual 7/12 | Casual 10/12 | Medical 8/8
    Pending Requests: count from ems_leave_requests where employee_id = EMP001 and status = pending
    Last Payslip: PKR 1,78,000 — March 2026

  My Attendance: last 7 days of EMP001's attendance from ems_attendance
  My Leave Requests: EMP001's leave requests from ems_leave_requests

═══════════════════════════════════════════════════════════════
FIX 20 — Edit employee must pre-fill with that employee's data
═══════════════════════════════════════════════════════════════

When HR clicks the Edit (pencil) icon on any employee row in the /employees table,
OR clicks [Edit] on any employee detail page /employees/:id:

The multi-step wizard at /employees/edit/:id must open with ALL fields
pre-filled with that employee's existing data from localStorage.

Step 1 pre-fills: name, father name, CNIC, DOB, gender, employee ID (read-only)
Step 2 pre-fills: all contact numbers and addresses
Step 3 pre-fills: bank name, account number, payment mode
Step 4 pre-fills: department, designation (filtered to correct dept), employment type,
                  job status, work location, work mode, reporting manager, shift,
                  timing (auto from shift), date of joining, commission toggle
Step 5 pre-fills: all salary component amounts for that employee
Step 6 pre-fills: medical information
Step 7 pre-fills: uploaded attachments status
Step 8 pre-fills: login credentials (username shown, password as placeholder)

When HR saves: updates the employee record in localStorage and navigates back
to /employees/:id (the detail page) showing the updated data with a success toast.

═══════════════════════════════════════════════════════════════
CRITICAL — AFTER ALL FIXES
═══════════════════════════════════════════════════════════════

After applying all 20 fixes:

1. Every action that modifies data must persist in localStorage.
   Refreshing the browser must NOT reset any changes.

2. All localStorage keys must be initialized with dummy data on first load
   if they don't already exist (seeding pattern).

3. The "Reset Demo Data" button in super_admin settings must clear all
   "ems_*" localStorage keys and reseed with the original dummy data.

4. Do not break anything that was already working correctly.
   Test every page after fixes.

5. All 20 fixes must be applied in one update — do not do them partially.
═══════════════════════════════════════════════════════════════