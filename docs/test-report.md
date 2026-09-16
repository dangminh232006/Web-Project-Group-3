# Test report

COS10026 Applied Web Project - Part 1. Tests executed 2026-09-16.

Everything below was actually run. Where a check could not be run, it is listed
under *Not tested* rather than being marked as passed.

---

## 1. Environment

| Item | Value |
|---|---|
| OS | Windows 11 Pro 26200 |
| Browser engine | Chromium via Playwright (headless), driven through MCP |
| Local server | `python -m http.server 8777`, served from the **parent** directory so the site sat at `/applied-web-project-part1/`, reproducing a GitHub Pages project subdirectory |
| HTML validator | Nu Html Checker, `vnu-jar` 26.9.16, run locally |
| CSS validator | W3C CSS Validator public API (`jigsaw.w3.org`), profile `css3` |

### Note on the unit's own validator

The course supplies `WebValidator.jar` (in `viewer/files/Tools/`). It **could not
be used** on this machine. It bundles Nu Html Checker 17.2.1 (2017), whose
`CssParser` class requires a JSR-223 JavaScript engine. Nashorn was removed from
the JDK in version 15, and this machine runs JDK 21, so the class fails at static
initialisation:

```
Caused by: java.lang.NullPointerException: Cannot invoke
"javax.script.ScriptEngine.eval(java.io.Reader)" because "engine" is null
    at nu.validator.datatype.tools.CssParser.<clinit>(CssParser.java:43)
```

A standalone current build of the same checker (`vnu-jar` 26.9.16) was used
instead. It is the same validator family and the same schema. If your tutor
requires output from `WebValidator.jar` specifically, run it on a machine with
JDK 8-14, or use the W3C web validators.

### The validators were proven to detect errors before being trusted

A "pass" only means something if the tool can fail. Both were checked against
deliberately broken input first:

| Tool | Deliberately broken input | Result |
|---|---|---|
| vnu | unclosed `<h1>`, `<img>` with no `alt`, `<blink>` | **6 errors, exit 1** |
| vnu | minimal valid page | **0 errors, exit 0** |
| W3C CSS | `colour: #333`, `margin: ;`, `display: flexx` | **invalid, 3 errors** |
| W3C CSS | `body { color: #333; margin: 0; }` | **valid, 0 errors** |

---

## 2. Validation results (final code)

| # | Check | Command | Result |
|---|---|---|---|
| TC-01 | HTML5 validity, `index.html` | `java -jar vnu.jar index.html` | **PASS** - 0 errors |
| TC-02 | HTML5 validity, `jobs.html` | as above | **PASS** - 0 errors |
| TC-03 | HTML5 validity, `apply.html` | as above | **PASS** - 0 errors |
| TC-04 | HTML5 validity, `about.html` | as above | **PASS** - 0 errors |
| TC-05 | CSS validity, `styles.css` | W3C API, profile css3 | **PASS** - `validity: true`, 0 errors |

`styles.css` returns **0 errors** and one level-0 warning: *"The property 'clip'
is deprecated"* - an accepted trade-off, see `decisions.md` D-11. The remaining
warnings are level-2 advisories ("you have set a color but no background-color",
"redefinition of X" for intentional responsive overrides) which the validator
emits for virtually any real stylesheet.

### Defect found and fixed during validation

**DEF-01** - `apply.html` used `autocomplete="street-address"` on a single-line
`<input>`. vnu rejected it: *"The autofill field name 'street-address' is not
allowed in this context"* - that token is for multi-line controls. Changed to
`address-line1`. Retested: 0 errors. **Fixed and retested.**

---

## 3. Structure and integrity checks

| # | Check | Result |
|---|---|---|
| TC-06 | Duplicate `id` attributes on any page | **PASS** - index 13 ids, jobs 11, apply 39, about 14; no duplicates |
| TC-07 | Every `<label for>` points at a real control | **PASS** |
| TC-08 | Every `aria-describedby` / `aria-labelledby` target exists | **PASS** |
| TC-09 | Every internal `href="#..."` target exists | **PASS** |
| TC-10 | Every local `href`/`src` file exists on disk | **PASS** - the only apparent miss, `images/team-photo.jpg`, appears solely as escaped example text inside `<code>`; there are **0** real `<img>` elements referencing it, so no broken image request is made |
| TC-11 | No JavaScript anywhere | **PASS** - 0 `<script>` tags, 0 inline `on*` handlers, 0 `.js` files |
| TC-12 | No Bootstrap / Tailwind / jQuery / React / Vue / CDN / web fonts | **PASS** - 0 matches |
| TC-13 | Only expected external URL | **PASS** - the sole external URL is the form `action` |
| TC-14 | Assets resolve under a repo subdirectory | **PASS** - `styles.css`, `logo.svg`, `bg-pattern.svg`, `workplace.svg` all HTTP 200 from `/applied-web-project-part1/` |

---

## 4. Responsive layout - measured at the five required widths

Each page was loaded in a same-origin iframe set to the exact CSS pixel width and
`document.documentElement.scrollWidth` compared with `clientWidth`.

### Before the fix - two real defects

| Page | 320px | 375px | 768px | 1024px | 1440px |
|---|---|---|---|---|---|
| index.html | **OVERFLOW** 427 > 305 | **OVERFLOW** 427 > 360 | ok | ok | ok |
| jobs.html | ok | ok | ok | ok | ok |
| apply.html | ok | ok | ok | ok | ok |
| about.html | **OVERFLOW** 388 > 305 | **OVERFLOW** 388 > 360 | ok | ok | ok |

**DEF-02** - the four-column data tables on `index.html` and `about.html` cannot
compress below their min-content width, so they forced the **whole page** to
scroll sideways on phones. This breaks the brief's responsive requirement and
WCAG 1.4.10 Reflow.

**Fix.** Each wide table is wrapped in
`<div class="table-scroll" tabindex="0" role="region" aria-label="...">` with
`overflow-x: auto`. The table now scrolls inside its own region instead of moving
the page. `tabindex="0"` is required so keyboard users can reach and scroll that
region, and the region has a visible focus outline.

### After the fix - retested

| Page | 320px | 375px | 768px | 1024px | 1440px |
|---|---|---|---|---|---|
| index.html | **PASS** 305 = 305 | **PASS** 360 = 360 | PASS | PASS | PASS |
| about.html | **PASS** 305 = 305 | **PASS** 360 = 360 | PASS | PASS | PASS |

Table region scrolls internally only where needed: `true` at 320 and 375,
`false` at 768 and 1440. Region `tabIndex` = 0 on both pages.

The only element reported outside the viewport at 320px is `#skip-link` at
`left: -9999px`, which is the intended off-screen position. Page scrollWidth is
unaffected.

---

## 5. Assessed CSS requirements - measured, not eyeballed

| # | Requirement | Measurement at 1440px | Result |
|---|---|---|---|
| TC-15 | `jobs.html` aside floats right | `getComputedStyle(aside).float` = `"right"` | **PASS** |
| TC-16 | aside is 25% wide | 252px inside a 1009px content box = **25.0%** | **PASS** |
| TC-17 | aside has margin, padding, border | margin `0 0 16px 24px`; padding `16px`; border `2px solid rgb(13,79,92)` | **PASS** |
| TC-18 | float is contained | container `display: flow-root`; aside right edge 1220 vs container inner right edge 1221 | **PASS** |
| TC-19 | float removed on narrow screens | `float` = `"none"` at 320, 375 and 768 | **PASS** |
| TC-20 | `apply.html` form uses Grid | `#application-form` `display: grid`; **1** column at 320/375, **2** columns at 768/1024/1440 | **PASS** |
| TC-21 | `index.html` CSS background graphic | `#home-hero` `background-image: url("images/bg-pattern.svg")`, HTTP 200 | **PASS** |
| TC-22 | `about.html` bordered figure, styled IDs, hex table colours, hover | `#group-photo` 4px solid #0d4f5c; `.student-id` styled; `#fun-facts` uses #0d4f5c / #f2f7f8 / #dbeceb; `tr:hover` present | **PASS** |

---

## 6. Form validation - all boundary cases from the brief

Run against the live page with `checkValidity()`. **31 of 31 cases matched the
expected result.**

| # | Case | Input | Expected | Actual | Result |
|---|---|---|---|---|---|
| TC-23a | Empty submission | all blank | blocked | blocked by **19** required controls | PASS |
| TC-23b | Reference 4 chars | `HD41` | invalid | invalid (patternMismatch) | PASS |
| TC-23c | Reference 5 chars | `HD417` | valid | valid | PASS |
| TC-23d | Reference 6 chars | `HD4178` | invalid | invalid | PASS |
| TC-23e | Reference non-alphanumeric | `HD-17` | invalid | invalid | PASS |
| TC-07 | First name 20 letters | 20 chars | valid | valid | PASS |
| TC-07b | First name 21 letters | 21 chars | invalid | invalid | PASS |
| TC-08 | First name hyphenated | `Anne-Marie` | invalid | invalid | PASS (documented limitation D-05) |
| TC-08b | First name apostrophe | `O'Brien` | invalid | invalid | PASS (documented limitation D-05) |
| TC-09 | First name diacritics | `Nguyễn` | invalid | invalid | PASS (documented limitation D-05) |
| TC-09b | Last name 20 / 21 letters | 20 / 21 chars | valid / invalid | valid / invalid | PASS |
| TC-14a | DOB valid | `04/09/1998` | valid | valid | PASS |
| TC-14b | DOB no leading zeros | `4/9/1998` | invalid | invalid | PASS |
| TC-14c | DOB ISO format | `1998-09-04` | invalid | invalid | PASS |
| TC-15a | DOB day 32 | `32/01/2000` | invalid | invalid | PASS |
| TC-15b | DOB month 13 | `01/13/2000` | invalid | invalid | PASS |
| **TC-16** | **DOB 31 February** | `31/02/2000` | **accepted** | **accepted** | **KNOWN LIMITATION D-06** |
| **TC-17** | **DOB 29 Feb, non-leap year** | `29/02/2001` | **accepted** | **accepted** | **KNOWN LIMITATION D-06** |
| TC-18a | Postcode leading zero | `0800` | valid | valid, zero preserved | PASS |
| TC-18b | Postcode 3 / 5 digits | `300` / `30000` | invalid | invalid | PASS |
| TC-18c | Postcode with letter | `30a0` | invalid | invalid | PASS |
| TC-19a | Email valid | `test.user@example.com` | valid | valid | PASS |
| TC-19b | Email no domain / incomplete | `test.user` / `test@` | invalid | invalid (typeMismatch) | PASS |
| TC-20a | Phone 7 digits | 7 digits | invalid | invalid | PASS |
| TC-20b | Phone 8 digits | 8 digits | valid | valid | PASS |
| TC-20c | Phone 12 digits, leading zero | `012345678901` | valid | valid, zero preserved | PASS |
| TC-20d | Phone 13 digits | 13 digits | invalid | invalid | PASS |
| TC-20e | Phone with spaces | `03 9000 1234` | invalid | invalid | PASS |
| TC-21a | Radio group before selection | none | invalid | invalid | PASS |
| TC-21b | Radio group after one selection | one | valid | valid | PASS |
| TC-22a | Optional textarea empty | blank | valid | valid, no `required` attribute | PASS |

### maxlength truncation, tested by simulated typing

| Field | Characters typed | `maxlength` | Resulting value length |
|---|---|---|---|
| firstName | 25 | 20 | **20** |
| streetAddress | 45 | 40 | **40** |
| suburb | 45 | 40 | **40** |
| jobReference | 8 | 5 | **5** |

### Skills checkboxes - the literal interpretation, verified

| # | Boxes ticked | Form valid? |
|---|---|---|
| TC-24 | 0 | **No** |
| TC-25 | 1 | **No** |
| TC-26 | 4 | **No** |
| TC-27 | 5 | **Yes** |

With every other field valid, the complete form is valid with 5 skills ticked and
invalid with 4. This confirms the behaviour described in `decisions.md` D-04: the
form enforces *all five*, not *at least one*.

---

## 7. POST endpoint test - synthetic data only

**TC-28.** POSTed made-up test data to
`https://mercury.swin.edu.au/it000000/formtest.php`.

- DNS: `mercury.swin.edu.au` resolves to `ictstudev1.cc.swin.edu.au`
  (136.186.123.54)
- Response: **HTTP 200**, 1,478 bytes, `text/html`
- The page returned is the unit's own *"HTML - Form Data Extraction Test"* script
  (meta author: Caslon Chua, Ken McInnes)

All 13 name/value pairs were echoed back correctly:

| # | Field | Value received |
|---|---|---|
| 1 | jobReference | `HD417` |
| 2 | firstName | `Testuser` |
| 3 | lastName | `Example` |
| 4 | dateOfBirth | `04/09/1998` |
| 5 | gender | `other` |
| 6 | streetAddress | `1 Test Street` |
| 7 | suburb | `Testville` |
| 8 | state | `VIC` |
| 9 | **postcode** | **`0800`** - leading zero preserved end to end |
| 10 | email | `test.user@example.com` |
| 11 | **phone** | **`0390001234`** - leading zero preserved end to end |
| 12 | skills | `html` |
| 13 | otherSkills | *(empty - optional field)* |

**No real personal data was used at any point.** The test values above are the
complete set that was sent.

### DEF-03 - silent data loss on the checkbox group

**TC-30.** POSTing five values under the plain name `skills`:

> received: `skills = version-control`

Only the **last** value arrived. Four ticked skills were silently discarded. This
is standard PHP behaviour for repeated field names without `[]`, and it would
have quietly corrupted every multi-skill application in Part 2.

**TC-31.** Same POST using `skills[]`:

> received: `skills = html, css, accessibility, responsive, version-control`

All five arrived. **Fixed:** `apply.html` now uses `name="skills[]"` on all five
checkboxes. Retested, and the page still validates with 0 errors.

---

## 8. Accessibility checks performed

| # | Check | Result |
|---|---|---|
| TC-32 | Skip link is first in tab order | **PASS** - order: skip-link, brand, Home, Jobs, Apply, About, then page content |
| TC-33 | Skip link hidden until focused, visible on focus, target exists | **PASS** - off-screen at `left: -9999px`, moves on focus, `#main-content` exists |
| TC-34 | Visible focus indicator | **PASS** - `:focus-visible { outline: 3px solid var(--c-focus); outline-offset: 2px }` applies to links, buttons, inputs, selects and textareas |
| TC-35 | Current page announced, not colour-only | **PASS** - `aria-current="page"` drives the highlight via `#site-nav a[aria-current="page"]` |
| TC-36 | Colour contrast (computed relative luminance) | **PASS** - all pairs exceed WCAG AA 4.5:1 and most exceed AAA 7:1 |
| TC-37 | Merged table cells have correct headers | **PASS** - `scope="col"`, `scope="colgroup"`, `scope="rowgroup"`, `scope="row"` used per cell role |
| TC-38 | Wide table reachable by keyboard after the reflow fix | **PASS** - scroll region has `tabindex="0"` and a focus outline |
| TC-39 | Reduced motion respected | **PASS** - `@media (prefers-reduced-motion: reduce)` present |

Measured contrast ratios:

| Pair | Ratio |
|---|---|
| Body text `#11263a` on `#f6f8f8` | **14.46:1** |
| Heading `#08333c` on `#ffffff` | **13.56:1** |
| Footer text `#e9f1f2` on `#08333c` | **11.83:1** |
| White on brand button `#0d4f5c` | **9.17:1** |
| Link `#8a3d12` on `#ffffff` | **7.62:1** |
| Hint text `#46586b` on `#ffffff` | **7.32:1** |

---

## 9. Visual inspection

Pages were rendered and screenshotted, not just read as source.

- `jobs.html` at 1440x1000 - confirmed the floated aside sits right at 25% with
  its border and spacing, the job card renders as a unit, the current nav item is
  highlighted, and the reference badge and salary styling read correctly.
- `about.html` at 375px, full page - confirmed the nav wraps cleanly, every
  placeholder is loudly highlighted, the bordered figure shows the dashed
  placeholder with no broken image, the fun-facts table scrolls in its own
  region, and the footer pending markers and fiction disclaimer are visible.

Screenshots were written outside the submission folder and are **not** part of
the ZIP.

---

## 10. Not tested

Listed honestly rather than assumed to pass.

| Area | Why not tested |
|---|---|
| The unit's `WebValidator.jar` | Cannot run on JDK 21 (see section 1). Re-run on JDK 8-14 if required. |
| The Accessibility Guideline PDF | Not present in the workspace; see `decisions.md` D-09. |
| Real screen readers (NVDA, JAWS, VoiceOver) | No assistive technology available in this environment. Semantics were checked structurally only. This is **not** a substitute; do a real screen-reader pass before submission. |
| Safari and Firefox | Only Chromium was available. |
| GitHub Pages deployment | No repository was supplied and no external action was authorised. |
| The Jira board | Not created; see `project-workflow.md`. |
| The group photograph | Not supplied, so file size and dimensions could not be measured. |
| Browser print output | Print CSS is present but was not visually proofed. |
| Automated accessibility scoring (axe, Lighthouse) | Not run. No accessibility score is claimed anywhere in this project. |
