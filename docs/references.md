# References and asset credits

COS10026 Applied Web Project - Part 1. Referencing style: APA 7 where applicable.

---

## 1. Third-party code used

**None.**

No code was copied or adapted from Stack Overflow, W3Schools, YouTube, a CMS
theme, a CSS framework, a component library or any other external source. The
HTML and CSS were written for this project.

Because of that, there are no source-attribution comments of the kind shown on the
Canvas *Unit Requirement: External Source Acknowledgment* page. If you add code
from anywhere during your own work, you **must** add a comment next to it naming
the source and the date accessed, and add a row to the table below.

| Where in the code | Source | Accessed |
|---|---|---|
| *(none yet)* | | |

---

## 2. Third-party assets used

**None.**

Every image in `images/` is original SVG source written for this project:

| File | What it is | Origin | Licence |
|---|---|---|---|
| `logo.svg` | Company logo mark | Written for this project | Group's own work |
| `bg-pattern.svg` | Decorative background pattern for the home page | Written for this project | Group's own work |
| `workplace.svg` | Abstract illustration of a product team | Written for this project | Group's own work |

No stock photography, icon set, web font or downloaded graphic is used. The site
loads **no** external resources at all, which is also why it works offline and
inside a GitHub Pages subdirectory without changes.

**Still to add:** `images/team-photo.jpg`, the group's own photograph. As the
group's own work it needs no external licence, but everyone in the photo should
agree to it being published.

---

## 3. Course materials referenced

These shaped decisions in the project. They are Canvas course materials for
COS10026, cited here as unit resources rather than as published works.

| Material | How it was used |
|---|---|
| *Applied Web Project Part 1 of 2 (Group Submission)* assignment page and its embedded requirements document | The source of every requirement. Quoted directly in `decisions.md` where the wording is ambiguous or self-contradictory |
| *Acknowledgement of Country* module | Shaped `decisions.md` D-07 and the decision not to name a Nation without checking |
| *Unit Requirement: GenAI Acknowledgment* | Defines the in-code acknowledgement format used in all four pages and `styles.css` |
| *Unit Requirement: External Source Acknowledgment* | Defines the format this file would use if external code were added |
| *IMPORTANT: Commenting CSS* | Source of the mandatory comment header block at the top of `styles.css` |
| *IMPORTANT: Code Commenting* | Shaped the commenting style, and the rule that comments explain *why* |
| *IMPORTANT: Naming Files and Folders* | Lowercase, hyphenated, no spaces, no special characters - followed throughout |
| *HTML Section and Aside Tags* | Shaped the use of `section` and `aside` on `jobs.html` |
| *Accessibility Guideline* PDF | **Not reviewed** - the file is referenced by the assignment but was not available. See `decisions.md` D-09 |

---

## 4. Standards and specifications consulted

| Standard | Relevance |
|---|---|
| HTML Living Standard (WHATWG) | Element and attribute validity, autofill token values, constraint validation |
| CSS specifications (W3C) | Grid, Flexbox, floats, media queries |
| Web Content Accessibility Guidelines (WCAG) 2.1 Level AA | Contrast 1.4.3, reflow 1.4.10, focus visibility 2.4.7, labels 3.3.2 |
| RFC 2606 | Reserved `.example` domain, used for the placeholder contact address so no real address is fabricated |
| RFC 4180 | CSV format used for `jira-backlog.csv` |

---

## 5. Tools used

| Tool | Purpose |
|---|---|
| Nu Html Checker, `vnu-jar` 26.9.16 | HTML5 validation |
| W3C CSS Validation Service, `jigsaw.w3.org` | CSS validation, profile CSS3 |
| Chromium via Playwright | Rendering, responsive measurement, form validation testing |
| Python `http.server` | Local server that reproduced a GitHub Pages subdirectory |
| `curl` | POST test against the Mercury form-data script |
| Claude, Anthropic Opus 5 | Drafting and testing - see `ai-use.md` |

None of these tools are shipped in the submission.

---

## 6. A note on APA 7

APA 7 applies to written academic work. This deliverable is a website plus
supporting notes, and it cites **no published literature** - the only sources are
the unit's own Canvas materials and technical specifications, listed above.

If your individual Project Self Report cites published sources, format those in
APA 7 in that document. There is nothing in this project that requires an APA
reference list, and inventing one would be worse than not having one.
