# SAHLAN RESULT BANK VERSION 3.0 — IMPORTANT SETUP

## Major changes

- Every student uses a separate Firebase Authentication account and a different password.
- Students can only read their own student document and their own results.
- Students cannot browse admission sessions or other student records.
- Students can change their own password.
- Students can apply to rewrite selected carry-over courses.
- Administrators can approve/reject applications and print the consolidated pending list.
- Course and result imports use deterministic IDs and skip existing records by default.
- Duplicate legacy course/result documents are cleaned during imports.
- Two consecutive completed academic years on probation produce the remark `Repeat`.
- Printing uses fixed A4 physical dimensions, giving the same page ratio from phone and laptop print services.

## Required Firebase setup

### 1. Authentication

Firebase Console → Authentication → Sign-in method:

- Enable Email/Password.
- Anonymous Authentication is no longer needed and may be disabled.

### 2. Publish the new Firestore rules

Copy the complete contents of `firestore.rules` into:

Firebase Console → Firestore Database → Rules → Publish

The new rules are required. Without them, students may be denied access or older broad access may remain.

### 3. Create student accounts

Log in as administrator and open:

Student Login Accounts → Create Missing Accounts

The system creates a separate Firebase account for every student without an `authUid`.

A CSV file is downloaded containing:

- Student name
- Matric number
- Personal password

Keep this CSV secure. Each password must be given only to the matching student.

Passwords are not stored in Firestore.

### 4. Existing Firebase student accounts

If Firebase reports `email-already-in-use` for an account that is not linked to a student document, open Firebase Authentication and delete that old account, then run Create Missing Accounts again.

### 5. Forgotten student passwords

Students can change passwords after login. Because the generated login email is internal, an administrator cannot send a normal email password reset. For a forgotten password:

- Firebase Console → Authentication → Users
- Locate the generated account
- Delete it
- Remove `authUid` and `loginEmail` from the matching student Firestore document
- Run Create Missing Accounts again

## Carry-over applications

Students see only outstanding carry-over courses from their latest result.

Administrator:

Carry-Over Applications → Print Pending List

The printed list is suitable for posting.

## Result and course imports

The default setting is `new records only`.

Tick the update checkbox only when intentionally correcting existing records.

## Printing

The print sheet is fixed to 194 mm, independent of phone or laptop viewport width.

For consistent output:

- Paper: A4
- Orientation: Portrait
- Scale: 100% or Default
- Margins: Default
- Background graphics: Enabled
