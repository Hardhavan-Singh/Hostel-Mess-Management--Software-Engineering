# 5. Use Case Narratives

The narratives below describe the principal functionalities of the proposed system. Each is traced to the functional requirements stated in Section 4.

---

## UC-01 — Log In

| | |
|---|---|
| **Use Case ID** | UC-01 |
| **Actors** | Student, Mess Committee Member, Warden, Contractor, Administrator |
| **Purpose** | To authenticate a user and present the functions permitted to their role |
| **Requirements** | FR1, FR2, FR3, NFR5 |

**Preconditions**  
The user holds an account created by the administrator.

**Main Flow**
1. The user opens the application and is presented with the login screen.
2. The user enters an identifier and password.
3. The system verifies the credentials against the stored account record.
4. The system determines the role assigned to the account.
5. The system presents the home screen corresponding to that role.

**Alternate Flow — A1: Incorrect credentials**  
At step 3, if the credentials do not match, the system reports that the identifier or password is incorrect and returns the user to step 2.

**Exception Flow — E1: Account deactivated**  
At step 3, if the account is marked deactivated, the system denies access and advises the user to contact the administrator.

**Postconditions**  
The user is authenticated and a session is established under the assigned role.

---

## UC-02 — View Daily Menu

| | |
|---|---|
| **Use Case ID** | UC-02 |
| **Actors** | Student |
| **Purpose** | To allow a student to see what is being served for a given meal |
| **Requirements** | FR5, FR8, NFR2, NFR3 |

**Preconditions**  
The student is logged in. A menu has been published for the date requested.

**Main Flow**
1. The student opens the menu view.
2. The system determines the current date and the meal nearest in time.
3. The system retrieves the published menu for that date and meal.
4. The system displays the items, indicating the meal and the serving time.
5. The system indicates whether the menu has been revised since publication.

**Alternate Flow — A1: Student selects another date**  
At step 2, the student may select a past or future date. The system retrieves and displays the menu recorded for that date.

**Exception Flow — E1: No menu published**  
At step 3, if no menu exists for the date and meal, the system states that the menu has not yet been published.

**Postconditions**  
The menu is displayed. No stored data is altered.

---

## UC-03 — Publish or Revise Menu

| | |
|---|---|
| **Use Case ID** | UC-03 |
| **Actors** | Mess Committee Member |
| **Secondary Actor** | Student (recipient of the notification) |
| **Purpose** | To record the menu for a date and meal, and to record any subsequent change to it |
| **Requirements** | FR6, FR7, FR8, FR9 |

**Preconditions**  
The user is logged in as a mess committee member.

**Main Flow**
1. The committee member selects a date and a meal.
2. The system displays the existing menu for that date and meal, if one exists.
3. The committee member enters or amends the list of items.
4. The committee member submits the menu.
5. The system stores the menu with the date, meal, author and time of publication.
6. Where an earlier version existed, the system retains it and marks the new entry as a revision.
7. Where the revision concerns the current day, the system notifies students.

**Alternate Flow — A1: Menu withdrawn**  
At step 3, the committee member may withdraw a published menu. The system retains the record and marks it withdrawn; it is not deleted.

**Exception Flow — E1: Date in the past**  
At step 4, if the selected date has passed, the system refuses the submission, since a record of what was served must not be altered retrospectively.

**Postconditions**  
The menu is recorded and available to students. Any earlier version is preserved.

---

## UC-04 — Submit Meal Rating

| | |
|---|---|
| **Use Case ID** | UC-04 |
| **Actors** | Student |
| **Purpose** | To record a student's assessment of a meal against the menu served |
| **Requirements** | FR10, FR11, FR12, FR13, NFR1, NFR10 |

**Preconditions**  
The student is logged in. A menu has been published for the meal. The meal has been served.

**Main Flow**
1. The student opens the rating view for the current meal.
2. The system displays the menu served for that meal.
3. The student selects a rating on a five-point scale.
4. The student optionally enters a comment.
5. The student submits the rating.
6. The system verifies that the student has not already rated this meal.
7. The system stores the rating against the student, the meal and the published menu.
8. The system confirms the submission and displays the current aggregate rating for the meal.

**Alternate Flow — A1: Rating without comment**  
Step 4 is omitted. The rating is stored alone.

**Exception Flow — E1: Meal already rated**  
At step 6, if a rating already exists for this student and meal, the system declines the submission and displays the rating previously recorded.

**Exception Flow — E2: Rating window closed**  
At step 5, if the permitted period for rating the meal has elapsed, the system declines the submission.

**Postconditions**  
The rating is stored and included in the aggregate for that meal. The student's identity is not disclosed in any aggregated view.

---

## UC-05 — Apply for Mess Rebate

| | |
|---|---|
| **Use Case ID** | UC-05 |
| **Actors** | Student |
| **Secondary Actor** | Warden (recipient of the application) |
| **Purpose** | To allow a student to claim a rebate for a period of absence, and to record the claim |
| **Requirements** | FR19, FR20, FR21, FR25, C2 |

**Preconditions**  
The student is logged in.

**Main Flow**
1. The student opens the rebate application form.
2. The student enters a start date, an end date and a reason for absence.
3. The student submits the application.
4. The system verifies that the start date is at least one day after the date of submission.
5. The system verifies that the period does not overlap an existing application.
6. The system stores the application with a unique reference and the status "pending".
7. The system displays an acknowledgement showing the reference and the number of days claimed.
8. The system places the application before the warden for a decision.

**Exception Flow — E1: Insufficient notice**  
At step 4, if the start date is not at least one day ahead, the system declines the application and states the notice required.

**Exception Flow — E2: Overlapping period**  
At step 5, if the dates overlap an existing application, the system declines the submission and displays the existing application.

**Postconditions**  
A rebate application exists with the status "pending" and is visible to both the student and the warden.

---

## UC-06 — Process Rebate Application

| | |
|---|---|
| **Use Case ID** | UC-06 |
| **Actors** | Warden |
| **Secondary Actor** | Student (recipient of the decision) |
| **Purpose** | To record the warden's decision on a rebate application and communicate it to the student |
| **Requirements** | FR22, FR23, FR24, NFR6, NFR9, C5 |

**Preconditions**  
The warden is logged in. At least one application holds the status "pending".

**Main Flow**
1. The warden opens the list of pending applications.
2. The system displays each application with the student, the dates, the number of days and the reason.
3. The warden selects an application.
4. The warden approves or rejects it, optionally recording a remark.
5. The system records the decision, the identity of the warden and the time.
6. Where the application is approved, the system computes the number of rebate days credited.
7. The system changes the status to "approved" or "rejected".
8. The system notifies the student of the decision and, where approved, of the days credited.

**Alternate Flow — A1: Partial approval**  
At step 4, the warden may approve a shorter period than that claimed. The systemm records both the period claimed and the period approved, together with the remark.

**Exception Flow — E1: Application withdrawn**  
At step 3, if the student has withdrawn the application in the interim, the system states this and returns the warden to step 1.

**Postconditions**  
The application holds a final status. The decision is recorded with its author and time, and the student has been notified.

---

## UC-07 — Register Complaint

| | |
|---|---|
| **Use Case ID** | UC-07 |
| **Actors** | Student |
| **Secondary Actor** | Mess Committee Member |
| **Purpose** | To record a complaint concerning the mess and make its progress visible to the student |
| **Requirements** | FR26, FR27, FR29 |

**Preconditions**  
The student is logged in.

**Main Flow**
1. The student opens the complaint form.
2. The student selects a category and enters a description.
3. The student optionally attaches a photograph.
4. The student submits the complaint.
5. The system stores the complaint with a unique reference, the date and the status "open".
6. The system displays the reference to the student.
7. The system places the complaint before the mess committee.

**Alternate Flow — A1: Complaint concerning a specific meal**  
At step 2, the student may associate the complaint with a meal served that day. The system records the link to the published menu.

**Exception Flow — E1: Attachment exceeds permitted size**  
At step 3, if the photograph exceeds the permitted size, the system declines the attachment and invites the student to submit the complaint without it.

**Postconditions**  
The complaint is recorded with the status "open" and is visible to the student and the committee.

---

## UC-08 — Update Complaint Status

| | |
|---|---|
| **Use Case ID** | UC-08 |
| **Actors** | Mess Committee Member |
| **Secondary Actor** | Student (originator of the complaint) |
| **Purpose** | To record the action taken on a complaint and close the loop with the student who raised it |
| **Requirements** | FR28, FR29, FR30, NFR9 |

**Preconditions**  
The committee member is logged in. At least one complaint is open or in progress.

**Main Flow**
1. The committee member opens the list of complaints, filtered by status or
   category.
2. The committee member selects a complaint.
3. The committee member changes its status to "in progress" or "resolved".
4. The committee member records a remark describing the action taken.
5. The system stores the change with the author and the time.
6. The system notifies the student who raised the complaint.

**Exception Flow — E1: Remark omitted on resolution**  
At step 4, if the status is set to "resolved" and no remark has been entered, the system declines the change, since a complaint may not be closed without a record of what was done.

**Postconditions**  
The complaint holds an updated status with a remark and an audit record, and the originating student has been informed.

---

## UC-09 — Conduct Menu Poll

| | |
|---|---|
| **Use Case ID** | UC-09 |
| **Actors** | Mess Committee Member, Student |
| **Purpose** | To establish student preference between menu items and record the action taken on the result |
| **Requirements** | FR15, FR16, FR17, FR18 |

**Preconditions**  
The committee member is logged in.

**Main Flow**
1. The committee member creates a poll, specifying a question, the options and a closing date.
2. The system publishes the poll to students.
3. Each student casts one vote.
4. The system records each vote, verifying that the student has not already voted.
5. At the closing date, the system closes the poll and computes the result.
6. The system displays the result to all students.
7. The committee member records the action taken on the result against the menu subsequently published.

**E xception Flow — E1: Student attempts to vote twice**  
At step 4, the system declines the second vote and displays the vote already recorded.

**Exception Flow — E2: Poll closes with no votes**  
At step 5, if no votes have been cast, the system closes the poll and records that no preference was established.

**Postconditions**  
The poll is closed, its result is visible to students, and the action taken on it is recorded.

---

## UC-10 — Generate Feedback Report

| | |
|---|---|
| **Use Case ID** | UC-10 |
| **Actors** | Mess Committee Member |
| **Secondary Actor** | Mess Contractor |
| **Purpose** | To produce aggregated evidence of student opinion for discussion with the contractor |
| **Requirements** | FR31, FR32, FR33, FR34, FR35, NFR10 |

**Preconditions**  
The committee member is logged in. Ratings or complaints exist for the period
selected.

**Main Flow**
1. The committee member selects a reporting period and a report type.
2. The system retrieves the ratings, complaints or rebate records for that period.
3. The system computes the average rating for each meal and identifies the  lowest-rated items.
4. The system compiles the complaint counts by category and status.
5. The system presents the report, with individual identities excluded.
6. The committee member makes the report available to the contractor.

**Alternate Flow — A1: Contractor views directly**  
The contractor, being logged in, may retrieve the rating and complaint reports without the committee member's intervention.

**Exception Flow — E1: No data for the period**  
At step 2, if no records exist for the selected period, the system states this and produces no report.

**Postconditions**  
The report is produced and is available to the committee and the contractor. No stored data is altered.