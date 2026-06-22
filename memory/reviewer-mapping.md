# Reviewer Mapping

Built from `src/content/doctors/*.mdx` frontmatter (`name`, `education`, `experience`) resolved against the `reviewer:` slug in illness/treatment/blog frontmatter. Used by Task 18 (Professional Input Briefs) to name reviewers and check specialty fit.

**Built:** 2026-06-22 (inaugural Task 18 run) · 50 doctor records parsed.

## Reviewers referenced by current YMYL + clinical-blog pages

| Reviewer slug | Name | Credentials | Exp (yrs) | Typical clusters (from 06-09 assignment commit `270cf0c`) |
|---|---|---|---|---|
| vishal-kasal | Dr. Vishal Kasal | (psychiatry) | 17 | Addiction (5 illness + 1 treatment) |
| dr-arun-kumar | Dr. Arun Kumar V | — | — | Mood / Geriatric / Neuromodulation (tDCS) |
| abhimanyu-chandak | Abhimanyu Chandak | — | — | Trauma / PTSD / EMDR |
| dr-akanksha-bhor | Dr. Akanksha Kashinath Bhor | — | — | Neurodevelopmental / child psych (ADHD, learning disability) |
| dr-thejus-kumar | Dr. Thejus Kumar B R | — | — | Bipolar / Schizophrenia / Psychosis |
| dr-sneha | Dr. Sneha | MD Psychiatry, MBBS | 11 | Personality, Eating; ADHD/Addiction/Anxiety/Dementia/OCD/Trauma |
| dr-rayani-m-dessa | Dr. Rayani M Dessa | M.Sc (Clinical Psychology), Psy.D. | — | Sleep / Biofeedback |
| krishna-k-r | Dr. Krishna K R | — | 22 | Anxiety / OCD / CBT / Psychotherapy / ERT |
| swarupa-mohan-udgiri | Dr. Swarupa Mohan Udgiri | PhD + M.Phil Psychiatric Social Work (NIMHANS) | — | Family / Couples / EFT / PPD / Perinatal |
| tirzah-johnson | Ms. Tirzah Johnson | — | — | Neurodevelopmental / child (conduct disorder) |
| tejal-jaiswal | Ms. Tejal Jaiswal | MPhil Clinical Psychology, MA Psychology, BA (Hons) Psychology | — | ACT / Positive Psychology |
| vindhya-shree | Ms. Vindhya Shree P K | MSc Clinical Psychology | — | DBT / REBT / Talk / Eclectic |
| suhita-saha | Ms. Suhita Saha | — | — | DBT / REBT / Talk / Eclectic |
| sufia-nusrat | Sufia Nusrat | — | — | Narrative / Identity |
| rangapriya-raghavan | Rangapriya Raghavan | — | — | Personality / Eating |
| navyashri-s | Ms. Navyashri S | — | — | Expressive (art + music) |

**Note:** Reviewer assignments are canonical from page frontmatter (set in commit `270cf0c`, 2026-06-09). When a brief is generated, the page's own `reviewer:` field is authoritative. Specialty-fit was confirmed against the assignment commit's clinical-fit map. Credentials shown as "—" were not present as a parseable `education:` field in the doctor record; resolve from the doctor profile page before publishing a byline.
