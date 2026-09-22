# SAHLAN Result Bank Version 4.1

## Major updates

- Added a separate **SAHLAN COLLEGE OF NURSING AND MIDWIFERY** college context.
- Nursing uses the supplied official logo (`assets/images/nursing-logo.jpg`). Nursing grade bands remain separate, while Nursing remarks are calculated from the number of outstanding carry-over courses rather than CGPA.
- Nursing is not displayed on the public welcome page. A nursing student is routed to the Nursing & Midwifery portal after secure matric-number/password login.
- Admin has a College switcher for Health Science & Technology vs Nursing & Midwifery. Lists, imports, courses, results, carry-over applications and account management are filtered by the selected college.
- Excel result import and course import support `NURSING`.
- Student result access can be locked/unlocked from Admin → Result Access Control. Locked students can sign in but cannot read results or submit carry-over applications.
- Firestore rules enforce the result lock at database level.
- Student Login Accounts displays the generated initial password. New generated passwords are saved in the admin-only `studentCredentials` collection. Existing accounts created before v4.1 cannot have their Firebase password recovered and will show `Not recorded` unless a new account is generated.
- Students are view-only: no result printing or transcript printing controls are shown. The result print function also checks for the admin role.
- Official results use a single **Registrar** signature only.
- Admin → Bulk Session Results can create one PDF containing one A4 page per student for the selected result session, with the student's First and Second Semester records on that page.
- Result print typography has been increased to use more of the A4 page.
- Health and Nursing grading bands and CGPA-based remarks are independently editable in Admin → School Settings.

## Firebase action required

After deploying the files, copy the included `firestore.rules` into:

Firebase Console → Firestore Database → Rules → Publish

The rules add protection for:

- `studentCredentials`
- `resultLocked` access
- carry-over access for locked students

## Important password note

Firebase Authentication does not expose a user's password for later retrieval. Version 4 stores the generated initial password separately for administrator access because this was requested for the portal. The collection is protected by Firestore rules so students cannot read it. If a student changes their password, the stored value remains the original generated password and is therefore only an initial-password record, not a live password mirror.

## Nursing logo

The Nursing & Midwifery logo has been replaced with the official logo supplied for this update at `assets/images/nursing-logo.jpg`.

## PDF library

Bulk PDF download uses jsPDF and html2canvas loaded from jsDelivr in `index.html`. Internet access is required for those CDN libraries when the bulk PDF feature is used.


### Version 4.1 changes requested
- Replaced the Nursing & Midwifery placeholder logo with the official logo supplied by the college.
- Nursing & Midwifery academic remarks now use outstanding carry-over count, not CGPA.
- Nursing carry-over remark ranges are editable by the Administrator under School Settings. Default ranges are 0 = Promoted, 1–2 = Probation, 3+ = Repeat; these can be changed to the college's approved policy.
