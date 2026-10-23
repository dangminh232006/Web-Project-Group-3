# Test report

COS10026 Applied Web Project - Part 1, Group 3. Updated 23 October 2026.
Results below distinguish the latest deployed-source validation from earlier browser checks.

## 1. Validation and deployed files (23 October 2026)

| Check | Tool | Result |
|---|---|---|
| `index.html`, `jobs.html`, `apply.html`, `about.html` | [W3C Nu HTML Checker](https://validator.w3.org/nu/) against each live URL | Each: 0 errors, 0 warnings |
| `styles.css`, `index.css`, `jobs.css`, `apply.css`, `about.css` | [W3C CSS Validator](https://jigsaw.w3.org/css-validator/), CSS level 3 + SVG profile | Each: valid, 0 errors |
| Four HTML pages and five CSS files | HTTP retrieval of the GitHub Pages files and comparison with committed source | All nine returned HTTP 200 and matched the audited commit `c265cea` |
| Internal page links and local assets | Local path checks | All referenced files exist |

The CSS request suppressed warnings; the result establishes zero errors, not zero warnings.
Windows working-tree line endings differ from the deployed files; the comparison used committed
Git content so line-ending conversion did not produce a false mismatch.

Earlier checks: on 18 October, all five stylesheets passed a local syntax parse, and Chrome
computed styles and element positions matched the pre-split version on four pages at 320,
768 and 1280 px (12 cases). These are historical regression results.

## 2. Responsive layout

On 20 October 2026, each page was loaded in Chrome at five widths and the page width
(`scrollWidth`) compared with the window width (20 cases). These measurements predate the
23 October About content changes; a fresh responsive walkthrough is tracked in Jira WWTP-42. Keyboard observations from
23 October are recorded below.

| Width | index | jobs | apply | about |
|---|---|---|---|---|
| 320 px | no page scroll | no page scroll | no page scroll | no page scroll |
| 375 px | no page scroll | no page scroll | no page scroll | no page scroll |
| 768 px | no page scroll | no page scroll | no page scroll | no page scroll |
| 1024 px | no page scroll | no page scroll | no page scroll | no page scroll |
| 1280 px | no page scroll | no page scroll | no page scroll | no page scroll |

At 320 and 375 px the two tables are wider than the screen; they scroll sideways inside their
`.table-wrapper` box (`overflow-x: auto`, Lecture 5) so the page itself never scrolls.

| Layout rule | Desktop | 768 px and below |
|---|---|---|
| `jobs.html` aside | `float: right; width: 25%` with margin, padding and border | stops floating, full width |
| Home hero | text and image side by side (Flexbox) | stacked |
| Application form | two-column Grid | one column |
| Footer (updated 20/10/2026) | four columns (Grid); two at 1024 px and below | two columns; one at 480 px and below |

## 3. Application form

On 7 October 2026, the rules were tested in Chrome with `checkValidity()`, setting valid and
invalid values. The 20 October end-to-end form check is recorded in section 6.

| Field | Value | Expected | Result |
|---|---|---|---|
| Job reference | `AFE26` | valid | valid |
| Job reference | `afe2` (4 characters) | invalid | invalid |
| Job reference | `AFE26X` (6 characters) | invalid | invalid |
| Job reference | `AF-26` (symbol) | invalid | invalid |
| First name | `Minh` | valid | valid |
| First name | `Anne-Marie` (hyphen) | invalid | invalid |
| First name | 20 letters | valid | valid |
| First name | 21 letters | invalid | invalid |
| First name | `Minh2` (digit) | invalid | invalid |
| Date of birth | `02/03/2006` | valid | valid |
| Date of birth | `2/3/2006` | invalid | invalid |
| Date of birth | `32/01/2000` (day 32) | invalid | invalid |
| Date of birth | `15/13/2000` (month 13) | invalid | invalid |
| Date of birth | `2006-03-02` | invalid | invalid |
| Postcode | `2000` | valid | valid |
| Postcode | `200`, `20000`, `20a0` | invalid | invalid |
| Phone | `0412345678` (10 digits) | valid | valid |
| Phone | `123456789012` (12 digits) | valid | valid |
| Phone | `1234567` (7), `1234567890123` (13) | invalid | invalid |
| Phone | `0412 345 678` (spaces) | invalid | invalid |
| Email | `a@b.com` | valid | valid |
| Email | `ab.com` | invalid | invalid |
| Street | empty | invalid | invalid |
| State | `Please select` (empty value) | invalid | invalid |
| State | `NSW` | valid | valid |

28 of 28 cases matched. Every input, select and textarea has a label. The text fields and state
selection are required; the gender radios form a required group. In Skills, only the HTML and
CSS checkbox is mandatory, and the other skill choices and Other skills textarea are optional.
This is the group's interpretation of the brief's all-fields-required wording, not confirmed
tutor acceptance; see `decisions.md` D-04.

Known limit: the date pattern checks the format and the ranges 01-31 and 01-12, not the calendar,
so `31/02/2000` is accepted. Calendar validation remains a limitation of this implementation;
server-side validation belongs to the later project stage.

### POST to the test script

On 7 October, the form was submitted to `https://mercury.swin.edu.au/it000000/formtest.php` with sample data.
The script returned HTTP 200 and echoed all 13 name/value pairs: `job_ref`, `first_name`,
`last_name`, `dob`, `gender`, `street`, `suburb`, `state`, `postcode`, `email`, `phone`,
`skills` (two values) and `other_skills`.

## 4. Links and images

All internal links (`index.html`, `jobs.html`, `apply.html`, `about.html`) and image paths are
relative, so the site works from the GitHub Pages sub-folder. The current image set contains the three site graphics and two supplied member portraits.
Their original files are retained; the former generated group-photo placeholder is no longer used.

The Google Map is in the shared footer of all four pages. Its rendering at desktop and phone
widths was checked on 20 October. The About page now uses two supplied portraits with a temporary caption. Separate portraits
do not satisfy the real full-group-photograph requirement.

## 5. Accessibility evidence and limits

The retained WAVE screenshots dated 23 October in the individual submission record show:

| Page | Errors | Contrast errors | Alerts | AIM score |
|---|---|---|---|---|
| Home | 0 | 0 | 3 | 10 |
| Jobs | 0 | 0 | 3 | 10 |
| Apply | 0 | 0 | 1 | 10 |
| About | 0 | 0 | 1 | 10 |

The alerts include redundant links: the brand and Home navigation target the same page, and
Jobs also has repeated application destinations. These are manual review prompts, not proof of
an inaccessible page. They remain recorded rather than being hidden as zero alerts. WAVE
screenshots establish the state when captured; they are not a screen-reader test or a complete
accessibility certification.

On 23 October, a live keyboard check traversed the four navigation links in order, activated
About with Enter, traversed the Apply controls with visible 3 px focus outlines, and toggled a
skill checkbox with Space in both directions. The source has since gained a Skip to main content
link on all four pages and a focusable main target. The About image alternatives and caption now accurately identify the two temporary portraits
and the pending full-group photograph. These changes require verification after publication.

Not yet verified in this audit: a screen-reader walkthrough, browsers other than Chrome, the
new skip link on the published site and a fresh responsive check after the latest edits. The
fresh viewport attempt on 23 October was blocked by the browser tool's paused document response;
no new responsive pass is claimed from that attempt. WWTP-42 remains In Progress.

### Review against the unit accessibility guideline (23 October)

The supplied *Accessibility in Microsoft Office & Webpages* by Armita Zarnegar was reviewed,
particularly PDF pages 3-5 (web, keyboard and vision guidance) and 10-12 (document checks).

| Guideline area | Source/evidence review | Remaining boundary |
|---|---|---|
| Accurate image alternatives | All image elements have alt text; two supplied portraits have accurate alternatives and a temporary caption | Real group photograph still needed |
| Heading structure and clear navigation | Semantic headings and consistent four-page navigation are present | Screen-reader navigation not tested |
| Form instructions and keyboard operation | Labels, fieldsets, legends, format hints and visible focus styles are present; native controls were traversed by keyboard | Published skip-link check and full responsive retest pending |
| Readable type and spacing | Shared body uses Helvetica/Arial sans-serif, scalable em sizes and 1.6 line height | No claim of testing every assistive reading configuration |
| Colour and contrast | WAVE evidence shows zero contrast errors; representative CSS text pairs calculated below | Gradient/image backgrounds still require visual review |
| Consistent layout and non-colour cues | Shared navigation/footer, labelled controls, underlined body links and written status/hints | No full accessibility conformance claim |
| Media alternatives | No audio/video player is used by this project | The embedded map is external content with a title and fallback link |

Representative sRGB contrast calculations from the current CSS use relative luminance and
`(lighter + 0.05) / (darker + 0.05)`. They supplement the WAVE screenshots rather than replacing
rendered-page checks.

| Text / background | Use | Contrast ratio |
|---|---|---|
| `#1d1d1f` / `#ffffff` | Body text | 16.83:1 |
| `#424245` / `#f5f5f7` | Secondary/footer text | 9.20:1 |
| `#0066cc` / `#ffffff` | Body links | 5.57:1 |
| `#ffffff` / `#0071e3` | Buttons and About table headings | 4.70:1 |
| `#f5f5f7` / `#1d1d1f` | Header navigation | 15.46:1 |
| `#1d1d1f` / `#d6e9ff` | About table hover text | 13.59:1 |

This review identifies the pending work rather than marking all accessibility requirements
complete. WWTP-43 remains In Progress until the published alt-text change is verified.

## 6. Form and footer regression checks (20/10/2026)

- W3C Nu HTML Checker: all four updated pages returned zero messages (0 errors, 0 warnings). All four also passed a strict local HTML5 parse; all five CSS files passed a local syntax parse.

- Chrome through the connected browser extension: all four pages at 320, 375, 768, 1024 and 1280 CSS px had no horizontal page overflow (20/20 cases). Every case contained four student email links and one map in the footer. The map rendered beside Pages on desktop.
- First/last name, street/suburb, state/postcode and email/phone pairs share top coordinates on desktop; text inputs and the select measure 48 px high. Radio padding is 0 px. The form stacks below 768 px.
- State and territory labels show full Australian names. All eight submitted abbreviations and native validation attributes remain unchanged.
- Submitted made-up values in Chrome to Mercury. A separate result tab displayed all 13 field names, including `state=ACT`. Closing it left the original form populated with `Test`, `ACT` and `Test only`; Clear form reset the fields and selections.
- Mercury's own Back button remains unavailable: its referenced `https://mercury.swin.edu.au/it000000/formutil.js` returned HTTP 404. The HTML-only new-tab behaviour avoids relying on it and is explained before the form.

- Class details are Wednesday, 09:00 to 12:00, tutor Thomas Harrison, as confirmed by the coordinator. Current 23 October source contains all four translated quotes and the styled fun-facts table; 12 cells for three members still need real details.

- About now includes a Selected project brief section describing the chosen Apple recruitment site, both advertised roles, the four pages and the HTML5/CSS3-only Part 1 scope.
