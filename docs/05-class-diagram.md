# 7. Class Diagram

## 7.1 Method

Candidate classes were identified by extracting the nouns appearing in the use
case narratives of Section 5. Candidates that proved to be attributes of another
class, synonyms of an existing class or entities outside the system boundary
were discarded. The classes retained are set out below each with the attributes
it must hold and the operations it performs derived from the steps of the
narratives in which it appears.

## 7.2 Classes

### User (abstract)

| Attributes | Operations |
|---|---|
| `- userId : String` | `+ login(id, password) : Boolean` |
| `- name : String` | `+ logout() : void` |
| `- email : String` | `+ changePassword(old, new) : Boolean` |
| `- passwordHash : String` | `+ getRole() : Role` |
| `- role : Role` | |
| `- isActive : Boolean` | |

Abstract because no user exists who is not one of the five specialisations
below. Holds what all users share: identity, credentials and role.

### Student (extends User)

| Attributes | Operations |
|---|---|
| `- rollNo : String` | `+ viewMenu(date, meal) : Menu` |
| `- hostelBlock : String` | `+ submitRating(menu, score, comment) : Rating` |
| `- roomNo : String` | `+ applyRebate(start, end, reason) : RebateApplication` |
| `- messId : String` | `+ registerComplaint(category, desc) : Complaint` |
| | `+ castVote(poll, option) : Vote` |

### CommitteeMember (extends User)

| Attributes | Operations |
|---|---|
| `- memberId : String` | `+ publishMenu(date, meal, items) : Menu` |
| `- tenureStart : Date` | `+ reviseMenu(menu, items) : Menu` |
| `- tenureEnd : Date` | `+ updateComplaintStatus(c, status, remark) : void` |
| | `+ createPoll(question, options, close) : Poll` |
| | `+ generateReport(type, from, to) : Report` |

### Warden (extends User)

| Attributes | Operations |
|---|---|
| `- employeeId : String` | `+ viewPendingApplications() : List<RebateApplication>` |
| | `+ approveRebate(app, days, remark) : void` |
| | `+ rejectRebate(app, remark) : void` |

### Contractor (extends User)

| Attributes | Operations |
|---|---|
| `- contractorId : String` | `+ viewReport(report) : Report` |
| `- organisation : String` | |
| `- contactNo : String` | |

### Administrator (extends User)

| Attributes | Operations |
|---|---|
| `- adminId : String` | `+ createAccount(details, role) : User` |
| | `+ deactivateAccount(user) : void` |
| | `+ assignRole(user, role) : void` |

### Menu

| Attributes | Operations |
|---|---|
| `- menuId : String` | `+ addItem(item) : void` |
| `- date : Date` | `+ removeItem(item) : void` |
| `- mealType : MealType` | `+ revise(items) : Menu` |
| `- publishedOn : DateTime` | `+ withdraw() : void` |
| `- version : Integer` | `+ getAverageRating() : Float` |
| `- status : MenuStatus` | |

`version` and `status` exist because FR7 requires that a revision preserve the
earlier menu rather than replace it.

### MenuItem

| Attributes | Operations |
|---|---|
| `- itemId : String` | `+ getAverageRating(from, to) : Float` |
| `- name : String` | |
| `- category : String` | |
| `- isVegetarian : Boolean` | |

Separate from Menu because the same item recurs across many menus, and FR32
requires the lowest-rated *items* to be identified, not merely the lowest-rated
meals.

### Rating

| Attributes | Operations |
|---|---|
| `- ratingId : String` | `+ submit() : Boolean` |
| `- score : Integer` | `+ isDuplicate(student, menu) : Boolean` |
| `- comment : String` | |
| `- submittedOn : DateTime` | |

### RebateApplication

| Attributes | Operations |
|---|---|
| `- applicationId : String` | `+ submit() : Boolean` |
| `- startDate : Date` | `+ calculateDays() : Integer` |
| `- endDate : Date` | `+ validateNotice() : Boolean` |
| `- reason : String` | `+ approve(days, remark, by) : void` |
| `- daysClaimed : Integer` | `+ reject(remark, by) : void` |
| `- daysApproved : Integer` | `+ withdraw() : void` |
| `- status : ApplicationStatus` | `+ getStatus() : ApplicationStatus` |
| `- appliedOn : DateTime` | |
| `- decidedOn : DateTime` | |
| `- decisionRemark : String` | |

`daysClaimed` and `daysApproved` are held separately because UC-06 A1 permits
the warden to approve a shorter period than the one claimed.

### Complaint

| Attributes | Operations |
|---|---|
| `- complaintId : String` | `+ register() : String` |
| `- category : String` | `+ updateStatus(status, remark, by) : void` |
| `- description : String` | `+ getStatus() : ComplaintStatus` |
| `- photoPath : String` | |
| `- status : ComplaintStatus` | |
| `- registeredOn : DateTime` | |
| `- handledBy : CommitteeMember` | |
| `- remark : String` | |
| `- resolvedOn : DateTime` | |

`handledBy` and `remark` satisfy NFR9 and enforce UC-08 E1, by which a complaint
cannot be closed without a record of the action taken.

### Poll

| Attributes | Operations |
|---|---|
| `- pollId : String` | `+ create() : void` |
| `- question : String` | `+ close() : void` |
| `- createdOn : DateTime` | `+ computeResult() : PollOption` |
| `- closingDate : Date` | `+ isOpen() : Boolean` |
| `- status : PollStatus` | |
| `- actionTaken : String` | |

`actionTaken` records what the committee did about the result, which is the
whole point of FR18 — a poll whose outcome is ignored reproduces the problem the
system exists to solve.

### PollOption

| Attributes | Operations |
|---|---|
| `- optionId : String` | `+ getVoteCount() : Integer` |
| `- optionText : String` | |

### Vote

| Attributes | Operations |
|---|---|
| `- voteId : String` | `+ cast() : Boolean` |
| `- castOn : DateTime` | `+ isDuplicate(student, poll) : Boolean` |

### Report

| Attributes | Operations |
|---|---|
| `- reportId : String` | `+ generate() : void` |
| `- type : ReportType` | `+ export(format) : File` |
| `- periodStart : Date` | `+ getSummary() : String` |
| `- periodEnd : Date` | |
| `- generatedOn : DateTime` | |

### Notification

| Attributes | Operations |
|---|---|
| `- notificationId : String` | `+ send() : Boolean` |
| `- message : String` | `+ markRead() : void` |
| `- sentOn : DateTime` | |
| `- isRead : Boolean` | |

## 7.3 Relationships

| From | Type | To | Multiplicity | Label |
|---|---|---|---|---|
| User | generalisation | Student, CommitteeMember, Warden, Contractor, Administrator | — | — |
| CommitteeMember | association | Menu | 1 → 0..* | publishes |
| Menu | association | MenuItem | 0..* ↔ 1..* | contains |
| Student | association | Rating | 1 → 0..* | submits |
| Menu | association | Rating | 1 → 0..* | receives |
| Student | association | RebateApplication | 1 → 0..* | submits |
| Warden | association | RebateApplication | 1 → 0..* | decides |
| Student | association | Complaint | 1 → 0..* | registers |
| CommitteeMember | association | Complaint | 1 → 0..* | handles |
| Complaint | association | Menu | 0..* → 0..1 | concerns |
| CommitteeMember | association | Poll | 1 → 0..* | creates |
| Poll | **composition** | PollOption | 1 → 2..* | offers |
| Student | association | Vote | 1 → 0..* | casts |
| PollOption | association | Vote | 1 → 0..* | receives |
| CommitteeMember | association | Report | 1 → 0..* | generates |
| Contractor | association | Report | 1 → 0..* | views |
| User | association | Notification | 1 → 0..* | receives |

## 7.4 Notation Notes

Generalisation is drawn as a solid line with a hollow triangular arrowhead
pointing to `User`. Associations are plain solid lines carrying a label and
multiplicities at each end. The relationship between `Poll` and `PollOption` is
a composition, drawn with a filled diamond at the `Poll` end, because an option
has no existence independent of the poll that offers it all other relationships
are ordinary associations, the participating objects being independently
meaningful.