# Decisions, source conflicts and open questions

COS10026 Applied Web Project - Part 1. Last updated 2026-09-16.

Every row below is either a **conflict found in the source material** or an
**interpretation we had to choose**. Nothing here is confirmed by a tutor unless
the Status column says so. Take the ones marked *Needs tutor confirmation* to
your tutorial before submission.

Source of truth used: the Canvas assignment *Applied Web Project Part 1 of 2
(Group Submission)* and its embedded requirements document, read from the course
export in this workspace.

---

## D-01. Allocated group code and industry are unknown - BLOCKING

**Conflict / gap.** The brief allocates a different industry to each group
(G01 Digital Health, G02 Smart City, G03 Sustainable Energy, G04 EdTech,
G05 E-Commerce, G06 Creative Digital Media) and says: *"You must tailor your
website content, job descriptions, company name, and design to your allocated
industry."* No group code was supplied to us.

**What we did.** We did **not** pick a group code. The site is built as an
explicitly provisional recruitment draft for a fictional company, *Harbourline
Digital*, described as a digital-services company hiring for its web team.

**Why this is a defensible starting point, not a substitute.** All six allocated
industries in the brief recruit the *same kind of people* - the blurbs for G01 to
G06 all mention digital platforms, web developers or designers. So the structure,
the two vacancies and the hiring process transfer to any of the six. What does
**not** transfer is the sector framing.

**What must change once the group code is known.** Roughly 12 blocks of text:

| Where | What to change |
|---|---|
| All 4 pages | Company name in the header, footer and `<title>`, and the slogan |
| `index.html` | Hero description paragraph, the two intro sentences |
| `jobs.html` | The "About the role" paragraph of each vacancy, and sector-specific responsibilities |
| `about.html` | The group code and industry lines in the nested list |
| `images/` | Logo colours if the group wants a different palette |

**Status: BLOCKED on group allocation.** Industry alignment is currently **not
met**, and must not be described as met.

---

## D-02. The two stated deadlines do not agree - NEEDS TUTOR CONFIRMATION

**Conflict, quoted exactly.**

| Source | Value |
|---|---|
| Requirements document inside the assignment page | "Due date: **Monday, Week 7 (20 Apr 2026) - 11:59pm**", repeated at the end as "Deadline: Monday, Week 7 (20 April 2026) - 11:59pm" |
| Same document, header | "**Semester 1, 2026**" |
| Canvas assignment metadata | due `2026-11-02T03:59:59+11:00`, available until `2026-11-09T03:59:59+11:00` |

**We have not chosen between them.** Both are recorded here as found.

**Observation, offered as an observation only.** The requirements document calls
itself a *Semester 1, 2026* document while the Canvas dates fall in
October-November. That is consistent with a Semester 1 document being reused in a
later teaching period, which would make the Canvas date the operative one. We
have **not** verified that, and it must not be relied on.

**Do not treat "available until" as an extension.** `2026-11-09` is the lock
date. A late-penalty policy may still apply after the due date.

**Action:** confirm the real due date with your tutor and write it into
`release-checklist.md`.

---

## D-03. The form endpoint link in the brief is malformed - RESOLVED BY TESTING

**Conflict.** The brief's apply.html section contains this markup, verbatim:

```html
<a href="formtest.php.">https://mercury.swin.edu.au/it000000/formtest.php"&gt;formtest.php.</a>
```

The `href` is the broken relative value `formtest.php.` (note the trailing full
stop). The *visible text* is `https://mercury.swin.edu.au/it000000/formtest.php`.
The anchor has clearly been pasted twice and mangled.

**What we did.** We used the **visible address** as the form action:

```html
<form id="application-form" method="post"
      action="https://mercury.swin.edu.au/it000000/formtest.php">
```

**What we verified.** We POSTed synthetic test data to that URL and it works. It
is the unit's own form-data echo script (the returned page is titled
*"HTML - Form Data Extraction Test"*, authored by Caslon Chua and Ken McInnes).
It echoed back all 13 name/value pairs correctly. Evidence: `test-report.md`
TC-28.

**Residual open question.** `it000000` looks like a placeholder for a Swinburne
Mercury account id. The path works as-is, but some tutors ask students to post to
their **own** Mercury account path. Ask, and change the one `action` attribute if
so.

**Status: working and verified. The `it000000` account id still needs tutor
confirmation.**

---

## D-04. "All fields except textarea must be required" vs a checkbox group - NEEDS TUTOR APPROVAL

**The ambiguity.** The brief lists *Skill list: Checkbox inputs* and then says
*"All inputs must have labels, and all fields except textarea must be required."*

Putting `required` on every checkbox is **not** the same as requiring at least
one selection:

| Interpretation | HTML needed | Result |
|---|---|---|
| Literal: every checkbox is required | `required` on all 5 boxes | The applicant must tick **all five** |
| Probably intended: at least one | none exists in HTML | Impossible without JavaScript, which the brief forbids |

HTML has no native "at least one of this group" constraint. There is no attribute
for it.

**What we did.** We implemented the **literal** reading: all five checkboxes carry
`required`. We then made the consequence visible on the page itself, so no
applicant is caught out:

> "Under the current settings every box below must be ticked before the form will
> submit. We read the brief literally here. If you meant 'tick at least one', tell
> us and we will change it - it cannot be done in HTML alone."

**What we did not do.** We did not pre-tick boxes to hide the problem, did not
swap the control type, and did not add JavaScript. We also do **not** claim the
form validates an at-least-one rule, because it does not.

**Verified behaviour** (`test-report.md` TC-24 to TC-27): with 0, 1 or 4 boxes
ticked the form is invalid; with all 5 ticked it is valid.

**Status: NEEDS TUTOR APPROVAL.** If the tutor confirms "at least one", the only
honest options within HTML and CSS are to drop `required` from the checkboxes and
state the expectation in text, or to defer the rule to server-side PHP in Part 2.

---

## D-05. "Max 20 alpha characters" excludes real names - IMPLEMENTED AS SPECIFIED

**The issue.** The brief says first and last name are *"Max 20 alpha characters"*.
Implemented literally as `pattern="[A-Za-z]{1,20}"`, which accepts only the 52
unaccented ASCII letters.

**Character set actually accepted:** `A`-`Z` and `a`-`z`. Nothing else.

**Names this rejects** (all tested, `test-report.md` TC-07 to TC-09):
`Anne-Marie` (hyphen), `O'Brien` (apostrophe), `Nguyễn` (diacritics), and any name
with a space.

**Why we left it.** The brief states the restriction, and we were told not to
silently redefine it. This is recorded as a known limitation rather than hidden.

**If the tutor allows a fix,** the minimal change that keeps the 20 character cap
while accepting real names is:

```html
pattern="[A-Za-zÀ-ÖØ-öø-ÿ' -]{1,20}"
```

**Status: implemented as specified; flagged as a real usability and inclusion
defect.**

---

## D-06. Date of birth: format checking is not calendar checking - KNOWN LIMITATION

**What the brief asks for.** `dd/mm/yyyy`.

**What we implemented.** A text input with:

```html
pattern="(0[1-9]|[12][0-9]|3[01])/(0[1-9]|1[0-2])/(19|20)[0-9]{2}"
```

**Why `type="text"` and not `type="date"`.** `type="date"` submits `yyyy-mm-dd`.
That would change the submitted format the brief specifies, so it was rejected.

**The limitation, stated plainly.** The pattern checks the *shape* and the numeric
*ranges*. It cannot check the calendar. Verified accepted-but-impossible dates
(`test-report.md` TC-16, TC-17): **`31/02/2000`** and **`29/02/2001`** both pass.

Real calendar validation needs server-side code (Part 2) or JavaScript (forbidden
here). We do **not** claim the field validates real dates.

**No age restriction was added.** The brief does not ask for one, so inventing a
minimum age would have been adding an unrequested rule.

---

## D-07. The Aboriginal and Torres Strait Islander element - INTERPRETATION

**What the brief allows.** *"a short Acknowledgement of Country, an inclusive
employment statement, a brief commitment to reconciliation or community
partnerships, or a statement encouraging applications from Aboriginal and Torres
Strait Islander peoples"* - and it must be thoughtful and clearly explained.
The rubric wording supplied to us also refers to an acknowledgement of country.

**What we chose.** An **inclusive employment statement plus a reconciliation
commitment**, with a section explaining why it belongs on a recruitment page and
three concrete process changes that follow from it.

**What we deliberately refused to invent:** a named Traditional Owner group or
Nation, a named community partner, an endorsement, or a statistic.

**Why.** The Canvas *Acknowledgement of Country* module is explicit: name the
correct Nation where possible, and *"An Acknowledgement of Country should not be
treated as a box-ticking exercise."* Guessing a Nation for a campus we cannot
confirm would be exactly the failure that page warns about.

**What the group must decide.** If your tutor expects a full Acknowledgement of
Country naming the Traditional Owners of your campus location, add it using the
AIATSIS Map of Indigenous Australia. A visible instruction to do this is on
`index.html`; remove that instruction once it is done.

**Status: NEEDS TUTOR CONFIRMATION** on whether a named acknowledgement is
required in addition to the inclusive employment statement.

---

## D-08. Search box behaviour is undefined - NEEDS TUTOR CONFIRMATION

**What the brief says, in full:** *"A search box with a button."* That is the
entire specification. No result behaviour is defined anywhere in the document.

**What we built.** A labelled search field and a submit button in a
`<form action="jobs.html" method="get" role="search">`. Submitting loads the full
vacancy list.

**What it does not do.** It does not filter by keyword. Keyword filtering needs
server-side code or JavaScript; the brief allows neither in Part 1. The typed text
is carried in the query string but is never used.

**How we avoided misleading anyone.** A visible note sits directly under the
field, wired to the input with `aria-describedby`, saying exactly that. We do not
describe a query string as working search.

**Status: acceptance criteria unknown.** Ask whether a navigation-only prototype
is acceptable for Part 1, or whether the search is expected to be implemented in
Part 2 with PHP.

---

## D-09. The Accessibility Guideline PDF could not be read - NOT REVIEWED

**What happened.** Both the group and individual assignment pages link to an
attachment: `AccessibilityInMSOffice&WEB (2).pdf`. It is listed in the course
export file manifest at 781,995 bytes, but the file was **not downloaded** into
this workspace - the `Uploaded Media` folder on disk does not contain it.

**Consequence.** The site has **not** been checked against that specific guideline
document. Any claim that it has would be false.

**What we used instead**, and it is not a substitute: the HTML and CSS
requirements in the brief itself, plus general WCAG 2.1 Level AA practice
(semantic landmarks, one `h1` per page, heading order, labels tied to controls,
`aria-describedby` for format hints, visible focus, contrast, reflow at 320px,
reduced-motion support).

**Action:** download the PDF from Canvas, read it, and re-check the four pages
against it. Until then, treat accessibility conformance as *self-assessed, not
verified against the unit's own guideline*.

---

## D-10. Checkbox field name changed to `skills[]` - IMPLEMENTED, EVIDENCE-BACKED

**What we found by testing.** With `name="skills"` on all five checkboxes, the
server receives **only the last ticked value**; the other four are silently
discarded. Tested against the unit's own Mercury echo script:

| Field name used | What the server actually received |
|---|---|
| `name="skills"` | `skills = version-control` (4 values lost) |
| `name="skills[]"` | `skills = html, css, accessibility, responsive, version-control` |

**What we did.** Used `name="skills[]"`. It is valid HTML5, it is the conventional
form for multi-value fields in PHP, and it is the only one of the two that does
not lose data. Evidence: `test-report.md` TC-30 and TC-31.

**How to revert** if your tutor prefers the plain name: change the five
`name="skills[]"` attributes in `apply.html` back to `name="skills"`, and accept
the data loss.

---

## D-11. `clip` vs `clip-path` in the visually-hidden helper - TRADE-OFF

The modern property for the screen-reader-only helper is `clip-path`. The W3C CSS
validator's `css3` profile does not recognise it and reports **an error**.
`clip` validates but is reported as **deprecated** (a warning).

**Chosen:** `clip: rect(0, 0, 0, 0)` - zero errors, one deprecation warning.
Both behave identically in every current browser for this purpose.

---

## D-12. Interview week and the individual due date - RECORDED, NOT RESOLVED

- The group brief says the individual interview is *"conducted during Week 6
  tutorial classes"*; the individual assignment page says *"during week 6 class"*.
  **No calendar dates are given anywhere.** We have not calculated or guessed
  them.
- The individual component's own page says *"Week 7, Friday - 11:59pm"*, while its
  Canvas metadata says `2026-11-02`, which is a Monday. This is a second
  inconsistency of the same kind as D-02.

**Action:** get the actual Week 6 tutorial date from your class timetable.

---

## D-13. Footer destinations that do not exist yet - DESIGN DECISION

The brief requires four footer items: Jira project, GitHub repository, live
GitHub Pages site, and an email link. Three of the four URLs were never supplied.

**What we did.** Rendered them as visible pending markers
(`<span class="pending">`) that read, for example, *"Jira project board (URL not
supplied yet)"* - **not** as `href="#"` links. A link that goes nowhere looks
finished and is not; a pending marker is honest and is impossible to miss during
review.

The email link is real markup pointing at `careers@harbourline.example`. The
`.example` top-level domain is reserved by RFC 2606 for documentation and can
never reach a real inbox, so no real address is fabricated.

**Update, same day.** Three of the four are now real links: the repository
(https://github.com/dangminh232006/Web-Project-Group-3), the live GitHub Pages site (https://dangminh232006.github.io/Web-Project-Group-3/), and the contact email, which is
now the group's Swinburne student address rather than the `.example` placeholder.

**Update: all four footer items are now live links.** The group supplied the Jira
board, so no pending markers remain anywhere on the site and the `.pending` CSS
rules were deleted as dead code.

**On the Jira URL specifically.** The link supplied was to a single issue,
`/browse/SAM1-11`. The brief asks for a *project* link, so the issue number was
dropped to give `/browse/SAM1`, which opens the project rather than one arbitrary
task. The project key `SAM1` was read directly from the supplied issue key - it
was not guessed. A board URL of the form `/jira/software/projects/SAM1/boards/1`
was deliberately **not** used, because the board id would have been invented.

**What could not be verified, and why.** The Atlassian connector available here
reaches only `cos20031-2026`, a different unit, with Confluence scopes and no Jira
scopes. Jira Cloud also returns HTTP 200 for nearly any path because it is a
single-page app, so a 200 proves only that the site responds. The group must open
the footer link while logged in and confirm it lands on the project.

**Note on the email.** It is now publicly visible on a deployed public site, so it
will be scraped by spam bots. That was a deliberate choice, preferred over an
undeliverable address. See `release-checklist.md`.
