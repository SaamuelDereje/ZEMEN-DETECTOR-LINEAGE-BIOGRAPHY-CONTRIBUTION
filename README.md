# ZEMEN-DETECTOR-LINEAGE-BIOGRAPHY-CONTRIBUTION
ZEMEN — DETECTOR LINEAGE & BIOGRAPHY CONTRIBUTION

Individual Contribution Portfolio — INSA Submission

Information	Details
Contributor	Samuel Dereje
Student ID	CTC-2910-26
GitHub	SaamuelDereje
Team	Team Sukuna
Project	Zemen
Contribution	Detector Lineage & Biography
Source Code	lineage.go
Demonstration	[Watch on YouTube]([YOUR VIDEO LINK])
1. Project Overview

Zemen is a security detection integrity and Ethiopian temporal-context platform designed to work with OpenSearch and Wazuh.

The project contains different modules that improve security monitoring, detection verification, and security analytics.

My individual contribution focuses on the Detector Lineage & Biography subsystem (internal/lineage/lineage.go).

2. What Is Detector Lineage?

Security detectors change over time. Rules are edited, switched on and off, and sometimes stop working, and usually nobody writes down why.

In Zemen, Detector Lineage gives every detector a narrative history, called its biography. It records:

When Zemen first saw the detector.
Every change to the detector's definition, found automatically by comparing snapshots.
Every status transition.
Replay regressions and recoveries.
Human-written reasons explaining why a change was made.

This lets a security team answer "what changed, when, and why?" instead of guessing.

3. My Contribution to Zemen
No.	Contribution Area	Description
1	Snapshot & Hashing	Flattens a detector definition and creates a SHA-256 fingerprint, ignoring volatile fields
2	Change Detection	Compares the current definition with the stored snapshot and lists the fields that changed
3	First-Seen Recording	Records an entry the first time Zemen observes a detector
4	Status Tracking	Records an entry when a detector's health status changes
5	Replay Integration	Logs regressions, recoveries and first-run failures between replay runs
6	Manual Reasons	Lets a human record why a change was made (zemen lineage add)
7	Biography Rendering	Builds a readable life story of a detector from its entries
8	Pending-Reason Tracking	Counts automatic definition changes that nobody has explained yet
4. How Lineage Works
Observe receives the current detectors and the latest health summary.
Each detector definition is flattened and hashed. Volatile fields (last_update_time, enabled_time, ui_metadata) are ignored so that harmless updates do not create noise.
The hash is compared with the stored snapshot.
If the detector is new, an auto-first-seen entry is written.
If the hash differs, an auto-definition-change entry is written with the changed fields, marked as waiting for a human reason.
If the health status changed, an auto-status-change entry is written.
The snapshot is updated for the next comparison.
After a replay run, RecordReplay compares the new results with the previous ones and logs regressions, recoveries and first-run failures.
Add stores a human-written reason, and Biography renders everything as a timeline.
5. Lineage Entry Types
Kind	Meaning
auto-first-seen	Zemen observed the detector for the first time
auto-definition-change	The detector's definition changed; a reason may still be needed
auto-status-change	The detector's health status changed
auto-replay-regression	A replay case passed before but now fails
auto-replay-recovered	A replay case that failed before now passes again
auto-replay-failed	A replay case failed on its very first run
manual	A person recorded the reason behind a change
6. Technical Implementation

Main file: internal/lineage/lineage.go

Key functions:

flatten / snap: turn a detector definition into sorted key-value pairs and a SHA-256 hash.
Observe: detects first-seen events, definition changes and status transitions.
Add: stores a human-written reason and rejects empty ones.
RecordReplay: logs replay regressions and recoveries.
ForDetector: returns a detector's entries, oldest first.
Biography: renders a detector's history as readable text.
PendingReasons: counts unexplained automatic changes.

The package works with other Zemen modules: config, health, indices, osclient, replay and secanalytics.

7. Video Demonstration

A 5-minute video showing the project, its key features and how it works:

Video: [YOUR VIDEO LINK]

8. Contribution Value

Detector Lineage makes detection changes accountable. It helps the project team:

See the full history of every detector.
Find out exactly which fields changed and when.
Notice when a detector that used to pass replay tests starts failing.
Require a human explanation for each definition change.
Keep an audit trail that supports trust in security monitoring.
9. Team Information

Team Name: Team Sukuna

No.	Full Name	CTC ID
1	Samuel Dereje	CTC-2910-26
2	Bekan Nura	CTC-2623-26
3	Baslel Getu	CTC-7059-26
4	Hundaol Dechassa	CTC-582-26
5	Yohannes Negero	CTC-312-26
6	Yilak Belayneh	CTC-2882-26
10. Conclusion

My contribution to Zemen focuses on the Detector Lineage & Biography feature.

It supports the project's objective of improving security detection reliability through traceable history, automatic change detection and clear records of why detectors changed.

I acknowledge that Zemen is a team project and that my individual contribution is focused on Lineage rather than the entire application.

Contributor: Samuel Dereje
ID: CTC-2910-26
