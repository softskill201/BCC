# Namami Digital Skills Academy — BCC Exam

Student exam: **[Open index.html](https://softskill201.github.io/BCC/)**  
Teacher panel: **[Open teacher.html](https://softskill201.github.io/BCC/teacher.html)**

## Features
- 26 bilingual questions: Unit 01 (Main Accessories of Computer) and Unit 02 (Fundamentals of Computer)
- 26-minute countdown, manual submit and auto-submit
- Student name, roll number, mobile and email
- Server-side score calculation and saved attempt/answer records
- Answer review, printable scorecard, JSON scorecard download
- QR code on the personal report card linking to the public [online verification page](https://softskill201.github.io/BCC/verify.html)
- Teacher login, search, review and CSV export
- Supabase Row Level Security protects student records

## Supabase project
- Project name: `Namami-BCC-Exam`
- Project ref: `jnfteavjywiqoatuwwhx`
- Region: Mumbai, India (`ap-south-1`)
- The database schema and question bank have been applied to the hosted project.
- The frontend contains only the Supabase **publishable** key. Never place a `service_role` or secret key in this repository.

## Enable GitHub Pages
1. Open repository Settings → Pages.
2. Under Build and deployment, choose **Deploy from a branch**.
3. Select branch `main`, folder `/ (root)`, and Save.
4. Wait for GitHub Pages to publish. Use the links at the top after publication.

## Set up the teacher account (required once)
The teacher panel is protected by Supabase Auth and a database allow-list. Merely knowing the page URL is not enough.

1. Open Supabase Dashboard for project `jnfteavjywiqoatuwwhx`.
2. Go to **Authentication → Users** and create the teacher account with the teacher's email and a strong password. Do not publish or share this password.
3. Copy the new user's UUID.
4. Open **SQL Editor** and run this query, replacing the UUID with the new Auth user's UUID:
   ```sql
   insert into public.bcc_teachers (user_id)
   values ('PASTE-AUTH-USER-UUID-HERE');
   ```
5. Open `teacher.html` and sign in with that account.

Only users explicitly added to `public.bcc_teachers` can query student result records. Do not enable unrestricted public signups for teacher accounts. Keep dashboard owner access and credentials private.

## Important notes
- Student records are private under Row Level Security; anonymous browsers can only read question text/options and submit through a database function that calculates the score on the server.
- The question key is stored server-side and is not included in the public question view.
- The public report verification endpoint returns only report ID, student name, marks, total, and submission time; it does not expose contact details, photos, or question-wise answers.
- A student receives a one-time review access code after submission. Ask students to keep it private.
- The question bank currently has 26 sample BCC questions; review them against your institute's final syllabus before using for a formal examination.
- The exam page uses a CDN for the Supabase JavaScript library and needs internet access while taking the exam. It is not an offline exam.
- Do not use real student records for testing until you have tested a sample submission and verified teacher access.
