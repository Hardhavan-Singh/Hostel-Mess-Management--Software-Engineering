# 4. Requirement Gathering and Analysis

## 4.1 Method Used

Requirements were gathered from two sources. The principal instrument was a structured questionnaire of fifteen
questions circulated online among the residents of Hostel D (Neeram Hall) and answered by 51 students. The questions were framed around the three problems identified in Section 3, so that each problem could be tested against the experience of the students who use the mess daily. In addition informal discussion was held with members of the hostel
mess committee in order to understand the administrative side of the process which students do not observe.

A questionnaire was preferred to interviews for the student population because the problems concern the routine experience of a large number of people rather than the working of any single role and a sample of this size indicates how widespread each difficulty is. Interviews were preferred for the committee because that side of the process involves few people and requires explanation rather than measurement.

### Limitations of the Survey

The 51 respondents represent approximately six per cent of the hostel's residents. As the questionnaire was circulated through hostel WhatsApp groups, the sample is likely to be weighted towards students who follow those groups actively and possibly towards those with stronger opinions about the mess. These limitations are stated here so that the requirements derived below are read with the appropriate degree of confidence.

## 4.2 Intended Users and Stakeholders

| Stakeholder | Role in the system |
|---|---|
| Student | Views the menu, rates meals, raises complaints, applies for rebates |
| Mess Committee | Publishes and revises the menu, conducts menu polls, reviews aggregated feedback, tracks complaints |
| Warden | Approves or rejects rebate applications; holds administrative oversight |
| Mess Contractor | Receives consolidated reports on ratings, complaints and expected attendance |
| System Administrator | Manages user accounts and role assignment |

## 4.3 Findings from the Survey

### Menu communication

Of the 51 respondents, 88.2 per cent rely on the hostel WhatsApp group to check the menu confirming it as the principal channel. The strongest single finding of the survey concerns the reliability of that channel: 92.2 per cent reported having reached the mess and found the food different from what was announced, 9.8 per cent of them describing his as a frequent occurrence. A smaller majority, 58.8 per cent reported having to scroll back through the group to
locate the menu.

Support for a dedicated menu page was positive but not unanimous: 56.9 per centsaid they would use one, 23.5 per cent were uncertain, and 19.6 per cent said they would not. This qualified response is recorded as it stands. It  indicates that a menu display alone is unlikely to be sufficient reason for a student to open the application and that the menu should therefore be presented alongside the functions students do actively want.

### Mess rebates

Only 13.7 per cent of respondents had ever applied for a mess rebate, and
15.7 per cent reported having been unsure how many rebate days were finally
credited to them. The number of students with direct experience of the process
is therefore small, and the difficulties described in Section 3 rest on a
correspondingly narrow base. One respondent remarked that rebates had not been
something they had considered until the survey raised the matter, despite
having been absent from the hostel on several occasions; this may indicate that
the present paper process discourages use or is not widely understood, though
the survey cannot establish this. Requirements concerning rebates are
consequently based principally on discussion with the mess committee rather
than on the student survey.

Notwithstanding the low usage, 52.9 per cent of respondents said they would
prefer to apply online and track the application, with a further 25.5 per cent
undecided.

### Feedback and complaints

Just under half of the respondents, 49 per cent, had used the QR-linked
feedback form. Of the whole sample, 37.3 per cent reported that no response or
observable change had followed their submission, against 17.6 per cent who
reported that something had.

The most significant finding of this section concerns willingness to
participate. Asked how likely they were to submit feedback if they expected no
response, 43.1 per cent gave the lowest rating and a further 23.5 per cent the
second lowest — two-thirds of respondents in total. By contrast, 66.7 per cent
said they would rate individual meals if doing so took less than fifteen
seconds. Taken together, these two results indicate that the present low
quality of feedback data is a consequence of the absence of a response, not of
student unwillingness, and that a short rating mechanism with visible
consequences would be used.

### Findings outside the scope of the proposed system

The open-ended question produced a clear result that does not concern
information management at all. The concerns raised most frequently were the
taste, quality and variety of the food, and crowding and queue lengths at meal
times. No software system can improve the cooking or shorten a queue, and these
concerns are therefore outside the scope of this project.

They are nevertheless relevant to it in two respects. First, they confirm that
students have substantial views about the mess which the present arrangement
does not capture in any usable form. Second, they indicate the purpose the
proposed system actually serves: it does not improve the food, but it records
what students think of it in an aggregated and dated form, so that the mess
committee can present evidence to the contractor in place of the anecdotal
reports on which it presently relies.

Two responses bear directly on the design. One described the present
arrangement in terms close to those of Section 3:

> "Everything is cluttered they should be in one application. We have separate
> QR for feedback, separate group for menu, they need to be integrated."

A second identified a failure of the feedback loop that the survey questions
had not anticipated, reporting that unpopular items remained on the menu
despite students having voted for their removal, and that such polls had since
ceased. This led to the addition of a menu poll facility to the proposed
system, described in the requirements below, by which the committee may conduct
a poll and record its outcome against the menu.

## 4.4 Functional Requirements

### Module 1 — User Management

| ID | Requirement |
|---|---|
| FR1 | The system shall allow a user to log in using a registered roll number or employee identifier and a password. |
| FR2 | The system shall assign each user one of five roles: student, mess committee member, warden, contractor or administrator. |
| FR3 | The system shall restrict the functions available to a user according to the assigned role. |
| FR4 | The system shall allow the administrator to create, modify and deactivate user accounts. |

### Module 2 — Menu Management

| ID | Requirement |
|---|---|
| FR5 | The system shall display the menu for the current date, identifying each of the three meals. |
| FR6 | The system shall allow a mess committee member to publish a menu for a specified date and meal. |
| FR7 | The system shall allow a published menu to be revised, retaining the previous version and recording the time of revision. |
| FR8 | The system shall retain all published menus, so that the menu served on any past date may be retrieved. |
| FR9 | The system shall notify students when a menu for the current day is revised. |

### Module 3 — Meal Feedback and Rating

| ID | Requirement |
|---|---|
| FR10 | The system shall allow a student to submit a rating on a five-point scale for a meal on the date it is served. |
| FR11 | The system shall allow an optional comment to accompany a rating. |
| FR12 | The system shall permit only one rating per student per meal. |
| FR13 | The system shall associate every rating with the menu published for that meal and date. |
| FR14 | The system shall display to students the aggregate rating of recent meals. |

### Module 4 — Menu Poll

| ID | Requirement |
|---|---|
| FR15 | The system shall allow a mess committee member to create a poll offering a choice between specified menu items. |
| FR16 | The system shall permit one vote per student per poll. |
| FR17 | The system shall display the outcome of a closed poll to all students. |
| FR18 | The system shall record the outcome of a poll against the menu subsequently published, so that the action taken on it is visible. |

### Module 5 — Rebate Management

| ID | Requirement |
|---|---|
| FR19 | The system shall allow a student to submit a rebate application specifying a start date, an end date and a reason. |
| FR20 | The system shall acknowledge receipt of an application immediately upon submission. |
| FR21 | The system shall reject an application submitted less than one day before the stated start date. |
| FR22 | The system shall present pending applications to the warden for approval or rejection. |
| FR23 | The system shall record the identity of the approving authority and the time of the decision. |
| FR24 | The system shall notify the student of the decision and, where approved, of the number of rebate days credited. |
| FR25 | The system shall allow a student to view the status and history of their rebate applications. |

### Module 6 — Complaint Management

| ID | Requirement |
|---|---|
| FR26 | The system shall allow a student to register a complaint under a defined category, optionally attaching a photograph. |
| FR27 | The system shall assign each complaint a unique reference and an initial status of "open". |
| FR28 | The system shall allow a mess committee member to change the status of a complaint to "in progress" or "resolved", recording a remark against the change. |
| FR29 | The system shall allow a student to view the current status of complaints they have registered. |
| FR30 | The system shall display the number of complaints registered under each category over a given period. |

### Module 7 — Reports and Analytics

| ID | Requirement |
|---|---|
| FR31 | The system shall generate a report of average meal ratings over a selected period. |
| FR32 | The system shall identify the meals and menu items receiving the lowest ratings in a selected period. |
| FR33 | The system shall generate a summary of complaints by category and status. |
| FR34 | The system shall generate a report of approved rebate days for a selected period. |
| FR35 | The system shall make the rating and complaint reports available to the mess contractor. |

## 4.5 Non-Functional Requirements

| ID | Category | Requirement |
|---|---|---|
| NFR1 | Usability | Submission of a meal rating shall be completable within fifteen seconds, since the survey establishes this as the condition of student participation. |
| NFR2 | Usability | The interface shall be usable on a mobile browser, this being the device on which students access the mess menu. |
| NFR3 | Performance | The menu for the current day shall be displayed within three seconds of a request under normal load. |
| NFR4 | Performance | The system shall support at least 200 concurrent users, meal times producing a concentrated pattern of use. |
| NFR5 | Security | Passwords shall be stored in hashed form and shall not be retrievable. |
| NFR6 | Security | Approval of a rebate application shall be permitted only to a user holding the warden role. |
| NFR7 | Reliability | A rating, complaint or rebate application, once acknowledged, shall not be lost. |
| NFR8 | Availability | The system shall be available at all times, and in particular during the hour preceding and following each meal. |
| NFR9 | Auditability | Every approval, rejection and status change shall be recorded with its author and time. |
| NFR10 | Privacy | Ratings and comments shall be presented to the committee and contractor only in aggregated form, so that individual students are not identifiable. |

## 4.6 Constraints

| ID | Constraint |
|---|---|
| C1 | Only registered residents of the hostel may hold a student account. |
| C2 | A rebate application must be submitted at least one day before the period of absence, in accordance with existing hostel rules. |
| C3 | A student may rate a given meal only once, and only on the date it is served. |
| C4 | The system is to operate on institutional infrastructure without recourse to paid third-party services. |
| C5 | Approval of rebates rests with the warden and cannot be delegated within the system. |

## 4.7 Assumptions and Dependencies

- Every resident student possesses a smartphone with internet access.
- The list of hostel residents is available from the institution and can be used to create student accounts.
- The mess committee is willing to publish the menu through the system rather than through WhatsApp.
- The mess contractor is willing to receive reports from the system.

## 4.8 Scope of the Proposed System

The system is concerned with the recording and communication of information about the mess. It does not extend to the preparation of food, the management of queues at meal times, the procurement of supplies, or the billing of mess fees, although the rebate figures it produces are intended to be used in billing. The concerns most frequently raised by respondents — the quality of the food and the length of queues — are accordingly outside its scope, as recorded in Section 4.3.