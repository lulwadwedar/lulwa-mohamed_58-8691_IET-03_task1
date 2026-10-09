# Task 1 — Inconsistencies and duplicates

**Name:** ______________________

**ID:** __-____

## Cleaning summary

I started with 39 rows. Looking first showed five problems: faculty, club and city were written many ways (`Information Engineering and Technology` vs `iet`, `Soccer` vs `Football`, `Alex` and `El Giza`); names and emails had extra spaces and mixed capitalisation; fee_paid was text (`yes`, `Y`, `1`, `false`...); and signed_up_at mixed `YYYY-MM-DD HH:MM` with `DD/MM/YYYY HH:MM`. I trimmed and lower-cased the categorical columns, mapped the leftovers with explicit dictionaries, and asserted that only canonical values remain. Names became single-spaced Title Case, emails trimmed lower-case, fee_paid a boolean. The slash dates are day-first because their first number reaches 18, so both formats parse into one datetime column. Removing exact duplicates dropped 3 rows (39 to 36); keeping one row per student_id + club dropped 4 more (36 to 32), and an assertion confirms the pair is unique. I kept the latest submission because students came back to mark the fee as paid, so the later row is the corrected one; latest is judged by the parsed timestamp, since comparing the raw text would rank `18/09/2026` before `2026-09-17`. Order matters: on the raw spellings only 2 of the 4 repeats are found (`Music` vs `music`, `Debate` vs `debate club` hide the rest), leaving 34 rows with 2 repeats still inside. Two different students are both named Mohamed Adel and share one email, so I deduplicated on student_id and never on name or email.
