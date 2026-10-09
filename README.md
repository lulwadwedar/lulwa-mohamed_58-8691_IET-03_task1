# Task 1 — Inconsistencies and duplicates

**Name:** Lulwa Mohamed Dwedar

**ID:** 58-8691

## Cleaning summary

I started with 39 rows. Looking first showed five problems: faculty, club and city were written in different ways (`Information Engineering and Technology` vs `iet`, `Soccer` vs `Football`, `Alex` and `El Giza`); names and emails had extra spaces and mixed capitalisation; `fee_paid` was text (`yes`, `Y`, `1`, `false`...); and `signed_up_at` mixed `YYYY-MM-DD HH:MM` with `DD/MM/YYYY HH:MM`. I first stripped extra spaces and converted the faculty, club and city values to lowercase, then used explicit dictionaries to map the remaining variants to their canonical values. I asserted that only the allowed canonical values remained. Names became single-spaced Title Case, and emails were trimmed and converted to lowercase. `fee_paid` was converted to a boolean. The slash dates are day-first because their first number reaches 18, so both formats parse into one datetime column. Removing exact duplicates dropped 3 rows (39 to 36); keeping one row per `student_id` + `club` dropped 4 more (36 to 32), and an assertion confirms the pair is unique. I kept the latest submission because students came back to mark the fee as paid, so the later row is the corrected one. The latest submission is judged by the parsed timestamp, since comparing the raw text would rank `18/09/2026` before `2026-09-17`. Order matters: on the raw spellings, only 2 of the 4 repeated sign-ups are found (`Music` vs `music`, and `Debate` vs `debate club` hide the rest), leaving 34 rows with 2 repeated pairs still inside. Two different students are both named Mohamed Adel and share one email, so I deduplicated using `student_id` and `club`, never by name or email.
