# Requirements traceability matrix

COS10026 Applied Web Project - Part 1. Last updated 2026-09-16.

Every requirement from the brief is mapped to the file and element that
implements it, the evidence that it works, and an honest status.

**Status values**

| Status | Meaning |
|---|---|
| **Verified** | Implemented and confirmed by a test that was actually run. Evidence referenced. |
| **Implemented** | Built and present, but not independently verified by a tool. |
| **Not tested** | Present, but no check was run. |
| **Needs information** | Cannot be completed without a fact only the group or tutor can supply. |
| **Blocked** | Cannot be completed at all until an external dependency exists. |

Rubric weighting used is the 70-point group breakdown supplied with this task
(Home 10, Jobs 10, Apply 10, About 10, CSS 10, Submission 5,
Usability/Accessibility 10, Jira 5). The rubric document itself was **not** in the
course export, so the wording of individual criteria could not be checked - only
the totals, which match the Canvas value of 70 points.

---

## A. index.html - Home (10 marks)

| # | Requirement | Implemented in | Evidence | Status |
|---|---|---|---|---|
| A1 | Company logo | `index.html` `.brand img` -> `images/logo.svg` (original SVG) | TC-14 asset 200 | **Verified** |
| A2 | Company name | `.brand__name` | visual check | **Verified** |
| A3 | Slogan | `.brand__slogan` - "Digital services people actually rely on" | visual check | **Verified** |
| A4 | Company description | `#home-hero` lead paragraphs | visual check | **Verified** |
| A5 | Company-related image | `.hero__figure img` -> `images/workplace.svg`, with descriptive `alt` | TC-14 | **Verified** |
| A6 | Common navigation menu | `#site-nav` - Home, Jobs, Apply, About in the same order on all 4 pages | TC-32 tab order | **Verified** |
| A7 | Footer: Jira project link | `#site-footer` pending marker | - | **Needs information** - board does not exist (D-13) |
| A8 | Footer: GitHub repository link | `#site-footer` -> https://github.com/dangminh232006/Web-Project-Group-3 | live link, HTTP 200 | **Verified** |
| A9 | Footer: live GitHub Pages link | `#site-footer` -> https://dangminh232006.github.io/Web-Project-Group-3/ | deployed, all pages HTTP 200 | **Verified** |
| A10 | Footer: email link | `a[href^="mailto:"]` -> `105716425@student.swin.edu.au` | TC-01 | **Verified** |
| A11 | At least one table using cell merging | `index.html` process table: `rowspan="2"` on Phase and Stage headers, `colspan="2"` on "What to expect", `rowspan="2"` on two Phase body cells | TC-01, TC-37 | **Verified** |
| A12 | Table is meaningful data, with caption and headers | `<caption>` plus `scope="col"`, `scope="colgroup"`, `scope="rowgroup"`, `scope="row"` | TC-37 | **Verified** |
| A13 | Search box with a button | `#site-search form` with labelled `input[type=search]` and submit button | TC-01 | **Verified** as a prototype |
| A14 | Search result behaviour | Navigates to `jobs.html`; no keyword filtering, stated visibly on the page | - | **Needs information** (D-08) |
| A15 | CSS background graphic | `#home-hero { background-image: url("images/bg-pattern.svg") }` | TC-21 | **Verified** |
| A16 | Embedded CSS example | `<style>` in `<head>`: `.hero__accent`, `.hero__figure img` | TC-01 | **Verified** |
| A17 | Inline CSS example | `style="max-width: 46ch;"` on the hero paragraph | TC-01 | **Verified** |

---

## B. jobs.html - Job descriptions (10 marks)

| # | Requirement | Implemented in | Evidence | Status |
|---|---|---|---|---|
| B1 | At least two job descriptions | `HD417` Front-End Developer, `HD892` Accessibility and Content Specialist | visual check | **Verified** |
| B2 | Reference number, exactly 5 alphanumeric | `.job__ref` - `HD417`, `HD892` | manual count | **Verified** |
| B3 | Job title and short description | `<h2>` + "About the role" section per job | visual check | **Verified** |
| B4 | Salary, unambiguous currency and period | "AUD 78,000 - 92,000 **per year**" and "AUD 72,000 - 84,000 **per year**", plus superannuation | visual check | **Verified** |
| B5 | Reporting line | `.job__meta` "Reporting line" definition per job | visual check | **Verified** |
| B6 | Key responsibilities | `ul.responsibilities` per job | visual check | **Verified** |
| B7 | Essential requirements, separate group | "Essential requirements" `<h3>` + `<ul>` per job | visual check | **Verified** |
| B8 | Preferable requirements, separate group | "Preferable requirements" `<h3>` + `<ul>` per job | visual check | **Verified** |
| B9 | Headings at two or more levels | `h1` > `h2` (job titles) > `h3` (subsections) | TC-01 | **Verified** |
| B10 | Multiple `<section>` elements | 2 job sections + intro + "How to apply" = 4 | TC-01 | **Verified** |
| B11 | At least one ordered list | `<ol>` - the five application steps | TC-01 | **Verified** |
| B12 | At least one unordered list | `<ul>` - responsibilities and requirements | TC-01 | **Verified** |
| B13 | At least one `<aside>` | `aside.job__aside` in each job card | TC-01 | **Verified** |
| B14 | Aside floats right at 25% with margin, padding, border | `@media (min-width: 64em) { .job__aside { float: right; width: 25% } }` | TC-15 to TC-18 - measured **25.0%**, `float: right`, contained | **Verified** |
| B15 | Responsive override removes the float | `float: none` below 64em; the base rule is full width | TC-19 - `none` at 320/375/768 | **Verified** |
| B16 | Apply link per vacancy | "Apply for HD417" / "Apply for HD892" | TC-09 | **Verified** |
| B17 | Realistic, concise, industry-appropriate content | Two full descriptions written as scenario content | - | **Needs information** - re-tailor to the allocated industry (D-01) |
| B18 | Embedded CSS example | `<style>`: `.job { border-left }`, `.salary` | TC-02 | **Verified** |
| B19 | Inline CSS example | `style="background-color: #fff3cd; ..."` on the closing-date phrase | TC-02 | **Verified** |

---

## C. apply.html - Application form (10 marks)

| # | Requirement | Implemented in | Evidence | Status |
|---|---|---|---|---|
| C1 | `method="post"` | `<form id="application-form" method="post">` | TC-28 | **Verified** |
| C2 | Posts to the Mercury test script | `action="https://mercury.swin.edu.au/it000000/formtest.php"` | TC-28 - HTTP 200, all 13 pairs echoed | **Verified**; `it000000` still needs confirming (D-03) |
| C3 | Job reference, exactly 5 alphanumeric | `pattern="[A-Za-z0-9]{5}"`, `minlength`/`maxlength` 5 | TC-23b to TC-23e | **Verified** |
| C4 | First name, alpha only, max 20 | `pattern="[A-Za-z]{1,20}"`, `maxlength="20"` | TC-07 to TC-09 | **Verified**; charset limitation documented (D-05) |
| C5 | Last name, alpha only, max 20 | same pattern | TC-09b | **Verified** |
| C6 | Date of birth, dd/mm/yyyy | `type="text"` + range-checked pattern | TC-14a to TC-15b | **Verified** for format; calendar validity **not** checked (D-06) |
| C7 | Gender radio buttons in fieldset + legend | `<fieldset><legend>Gender</legend>` with 4 radios sharing `name="gender"` | TC-21a, TC-21b | **Verified** |
| C8 | Street address, max 40 | `maxlength="40"` | truncation test 45 -> 40 | **Verified** |
| C9 | Suburb/town, max 40 | `maxlength="40"` | truncation test 45 -> 40 | **Verified** |
| C10 | State dropdown: VIC NSW QLD NT WA SA TAS ACT | `<select id="state">` with all 8, plus an empty prompt so `required` works | TC-03 | **Verified** |
| C11 | Postcode, exactly 4 digits | `pattern="[0-9]{4}"`, `type="text"` + `inputmode="numeric"` | TC-18a to TC-18c; `0800` survived the POST | **Verified** - leading zeros preserved |
| C12 | Email, valid format | `type="email"` | TC-19a, TC-19b | **Verified** |
| C13 | Phone, 8 to 12 digits | `pattern="[0-9]{8,12}"`, `type="text"` | TC-20a to TC-20e; `0390001234` survived the POST | **Verified** - leading zeros preserved |
| C14 | Skill list as checkboxes | 5 checkboxes, `name="skills[]"` | TC-30, TC-31 | **Verified**; name changed to prevent data loss (D-10) |
| C15 | Other skills textarea | `<textarea id="otherSkills">`, no `required` | TC-22a | **Verified** |
| C16 | Every input has an associated label | visible `<label for>` on every control; `<legend>` for each group | TC-07 integrity check | **Verified** |
| C17 | All fields except textarea are required | 19 required controls block an empty submission | TC-23a | **Verified**; checkbox reading needs approval (D-04) |
| C18 | HTML5 validation with patterns | patterns on 6 fields, `type="email"` on 1 | 31/31 boundary cases matched | **Verified** |
| C19 | Form layout uses Flexbox or Grid | `#application-form { display: grid }` + `.field { display: flex }` | TC-20 - 1 column at 320/375, 2 at 768+ | **Verified** |
| C20 | Meaningful `name` attributes and unique IDs | 13 distinct POST field names; 39 unique ids | TC-06, TC-28 | **Verified** |
| C21 | Format instructions linked to controls | `.hint` paragraphs wired with `aria-describedby` | TC-08 | **Verified** |
| C22 | Labels not replaced by placeholders | every control has a real `<label>`; placeholder used only as an extra example | TC-03 | **Verified** |
| C23 | Embedded CSS example | `<style>`: `.req`, `.hint code` | TC-03 | **Verified** |
| C24 | Inline CSS example | `style="max-width: 10rem;"` on the postcode input | TC-03 | **Verified** |

---

## D. about.html - Team page (10 marks)

| # | Requirement | Implemented in | Evidence | Status |
|---|---|---|---|---|
| D1 | Group name and class day/time in a nested list | `#class-details` - `<ul>` with a nested `<ul>` | TC-04 | **Implemented**; values are placeholders - **Needs information** |
| D2 | Member contributions in a definition list | `dl#contributions` with `<dt>` per member and `<dd>` per fact | TC-04 | **Implemented**; content **Needs information** |
| D3 | Quote from each member in their first language | `.quote` paragraph per member | - | **Needs information** - must come from each member; a `lang` attribute must be added with the quote |
| D4 | English translation of each quote | `.quote__translation` per member | - | **Needs information** |
| D5 | Group photo, not individual portraits | `<figure id="group-photo">` currently holds a CSS placeholder | - | **NOT MET** - no photograph supplied |
| D6 | Photo under 300KB | - | - | **Not tested** - no file to measure |
| D7 | Photo inside `<figure>` with a caption | `<figure>` + `<figcaption>` present and ready | TC-04 | **Verified** (structure) |
| D8 | Figure has a visible border | `#group-photo { border: 4px solid #0d4f5c }` | TC-22 | **Verified** |
| D9 | Student IDs styled | `.student-id` - monospace, letter-spaced, white on `#0d4f5c` | TC-22 | **Verified** |
| D10 | Fun facts table with a caption | `#fun-facts` with `<caption>Fun facts about the team</caption>` | TC-04 | **Verified** (structure); rows **Needs information** |
| D11 | Table uses hexadecimal colours | `#0d4f5c`, `#ffffff`, `#f2f7f8`, `#dbeceb`, `#08333c` | TC-22 | **Verified** |
| D12 | Table has a hover effect | `#fun-facts tbody tr:hover` | TC-22 | **Verified** |
| D13 | Hover does not hide information from keyboard users | hover changes background only; all content readable without it | TC-38 | **Verified** |
| D14 | No broken image request while the photo is missing | 0 `<img>` elements referencing `team-photo.jpg`; placeholder drawn in CSS | TC-10 | **Verified** |
| D15 | Embedded CSS example | `<style>`: `.tbd` placeholder marker | TC-04 | **Verified** |
| D16 | Inline CSS example | `style="min-height: 15rem;"` on the photo placeholder | TC-04 | **Verified** |

---

## E. CSS and styling (10 marks)

| # | Requirement | Implemented in | Evidence | Status |
|---|---|---|---|---|
| E1 | External stylesheet `styles.css` | one file, linked from all 4 pages | TC-05 | **Verified** |
| E2 | At least one embedded CSS example on **every** page | `<style>` block in all 4 `<head>`s | A16, B18, C23, D15 | **Verified** |
| E3 | At least one inline CSS example on **every** page | one `style` attribute per page | A17, B19, C24, D16 | **Verified** |
| E4 | Inline/embedded CSS not overused | exactly 1 inline attribute and 1 small `<style>` block per page; everything else external | manual count | **Verified** |
| E5 | Clear comments in `styles.css` | unit-mandated header block plus 8 numbered section banners | TC-05 | **Verified** |
| E6 | Wide range of selectors | see the selector table below | TC-05 | **Verified** |
| E7 | Responsive layout in `styles.css` | mobile-first base + `min-width: 40em` and `min-width: 64em` breakpoints | section 4 of the test report | **Verified** |
| E8 | Accessibility practices in `styles.css` | focus-visible ring, skip-link, `.visually-hidden`, reduced motion, contrast, reflow | TC-32 to TC-39 | **Verified** |
| E9 | CSS validates | W3C CSS Validator, profile css3 | TC-05 - 0 errors | **Verified** |

### Selector variety actually used (E6)

| Selector type | Example in `styles.css` | Purpose |
|---|---|---|
| Element | `body`, `table`, `legend`, `fieldset` | base typography and form chrome |
| Class | `.btn`, `.job__aside`, `.student-id`, `.table-scroll` | reusable components |
| ID | `#site-nav`, `#home-hero`, `#application-form`, `#fun-facts` | one-per-page landmarks |
| Descendant combinator | `#site-nav a` | links inside the nav only |
| Child combinator | `.responsibilities > li` | direct list items only |
| Adjacent sibling combinator | `h2 + p` | lead paragraph after a heading |
| Attribute | `a[href^="mailto:"]`, `input[type="checkbox"]`, `#site-nav a[aria-current="page"]` | style by role, not by extra classes |
| Pseudo-class (state) | `:hover`, `:focus-visible`, `:focus` | interaction feedback |
| Pseudo-class (form) | `:required:invalid`, `:required:valid` | live validation feedback |
| Pseudo-class (structural) | `#fun-facts tbody tr:nth-child(even)` | zebra striping |
| Pseudo-element | `a[href^="mailto:"]::before`, `.pending::after` | generated content |
| Grouping | `h1, h2, h3, h4` | shared heading rhythm |
| Universal | `*, *::before, *::after` | box-sizing reset |
| At-rules | `@media screen and (min-width: ...)`, `@media (prefers-reduced-motion: reduce)`, `@media print` | responsive and user preference |

---

## F. Usability and accessibility (10 marks)

| # | Requirement | Evidence | Status |
|---|---|---|---|
| F1 | All pages validate as HTML5 | TC-01 to TC-04 - 0 errors | **Verified** |
| F2 | Semantic tags used | `header`, `nav`, `main`, `section`, `aside`, `figure`, `figcaption`, `footer`, `dl`, `fieldset`, `legend`, `caption` | **Verified** |
| F3 | Logical heading hierarchy | one `h1` per page, `h2`/`h3` in order, no level skipped | **Verified** |
| F4 | Consistent navigation, same order everywhere | TC-32 | **Verified** |
| F5 | Current page indicated accessibly | TC-35 - `aria-current="page"` | **Verified** |
| F6 | Skip link | TC-33 | **Verified** |
| F7 | Keyboard focus visible | TC-34 | **Verified** |
| F8 | Meaningful alt text; decorative images handled | `alt` on logo and hero illustration; background pattern is a CSS background, so it needs no alt | **Verified** |
| F9 | Table headers and captions | TC-37 | **Verified** |
| F10 | Form labels | TC-16 in section C | **Verified** |
| F11 | Readable contrast | TC-36 - lowest measured 7.32:1 | **Verified** |
| F12 | Zoom and reflow to 320px | section 4 - no horizontal page scroll at 320px | **Verified** |
| F13 | Reduced motion support | TC-39 | **Verified** |
| F14 | Native semantics preferred over ARIA | ARIA used only for `aria-current`, `aria-describedby`, `aria-labelledby`, `role="search"`, and the scroll region | **Verified** |
| F15 | Checked against the unit's Accessibility Guideline PDF | - | **NOT DONE** - file unavailable (D-09) |
| F16 | Screen reader testing | - | **Not tested** - no assistive technology available |
| F17 | Inclusive element for Aboriginal and Torres Strait Islander peoples, clearly explained | `#acknowledgement` on `index.html` | **Implemented**; scope needs confirming (D-07) |

---

## G. Submission (5 marks)

| # | Requirement | Status |
|---|---|---|
| G1 | Four pages at the project root | **Verified** - `index.html`, `jobs.html`, `apply.html`, `about.html` |
| G2 | Single external stylesheet at the root | **Verified** - `styles.css` |
| G3 | Relative paths that survive a repo subdirectory | **Verified** - TC-14 |
| G4 | No JavaScript, Bootstrap or other libraries | **Verified** - TC-11, TC-12 |
| G5 | Deployed on GitHub Pages | **Verified** - https://dangminh232006.github.io/Web-Project-Group-3/ building from `main` at root; all four pages and every asset return HTTP 200 |
| G6 | GitHub repository link in `index.html` | **Verified** - https://github.com/dangminh232006/Web-Project-Group-3 in the footer of all four pages |
| G7 | ZIP submitted via Canvas | **Blocked** - ZIP is built locally; submitting is a human action |
| G8 | Group Agreement submitted **before** project work | **Needs information** - see `group-agreement-template.md`; must not be backdated |
| G9 | GenAI use acknowledged in code comments | **Verified** - comment block in all 4 pages and in `styles.css`, per the unit requirement |
| G10 | External sources acknowledged | **Verified** - `references.md`; no third-party code or assets were used |
| G11 | Each member develops at least one page and its CSS | **Needs information** - `contributions.md` is unfilled |

---

## H. Jira (5 marks)

| # | Requirement | Status |
|---|---|---|
| H1 | Jira used to manage the project | **Blocked** - no Jira instance or URL supplied; nothing was created |
| H2 | Epics, user stories and tasks | **Implemented as a proposal only** - `jira-backlog.csv` |
| H3 | At least two sprints | **Implemented as a proposal only** - `project-workflow.md` |
| H4 | Board shared with the tutor | **Blocked** |

> A CSV file is not a populated Jira board. Until the issues exist in a real
> project and the tutor has access, H1 to H4 score nothing.

---

## Summary of what is not yet met

| Blocker | Rubric area |
|---|---|
| Group code and industry not allocated | B17, D1 - affects Jobs and About |
| Group photograph missing | D5, D6 - About |
| Member names, IDs, contributions, quotes, fun facts missing | D1 to D4, D10, G11 - About and Submission |
| Jira board not created | H1 to H4 - all 5 Jira marks |
| ~~GitHub repository and Pages deployment~~ | **Resolved** - A8, A9, G5, G6 now verified |
| Accessibility Guideline PDF not reviewed | F15 |
| Skills checkbox interpretation unapproved | C17 |
| Due date unresolved | G7 |
