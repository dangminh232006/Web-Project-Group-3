# Harbourline Digital - recruitment website

COS10026 Web Technology Project
**Assessment 2: Applied Web Project - Part 1** (group component, 70 marks)

A static recruitment website built with HTML5 and CSS3 only. No JavaScript, no
frameworks, no build step, no external requests.

> ## Status: NOT READY TO SUBMIT
>
> The code is complete, validates, and is **deployed live**. The **human content
> does not exist yet** - no group code, no member names, no group photo, and no
> Jira board. Start at **`docs/release-checklist.md`**, which lists every blocker.
>
> - Live site: https://dangminh232006.github.io/Web-Project-Group-3/
> - Repository: https://github.com/dangminh232006/Web-Project-Group-3
>
> `Harbourline Digital` is a **fictional company** invented for this assessment.
> No vacancy, salary or statement on the site describes a real employer.

---

## Confirmed industry

**None. The group code was never supplied**, so the required industry tailoring
(G01 Digital Health, G02 Smart City, G03 Sustainable Energy, G04 EdTech,
G05 E-Commerce, G06 Creative Digital Media) **has not been done.**

The site is currently a provisional digital-services recruitment draft. That is a
deliberate, documented position, not an oversight - see `docs/decisions.md` D-01,
which lists exactly which blocks of text to rewrite once the allocation is known.
Do not describe the current content as industry-aligned.

---

## Project structure

```
applied-web-project-part1/
├── index.html          Home: identity, merged-cell table, search, inclusion statement
├── jobs.html           Two full vacancies, floated aside
├── apply.html          13-field validated application form
├── about.html          Team page (placeholders throughout)
├── styles.css          The single external stylesheet, 8 commented sections
├── images/
│   ├── logo.svg        Company logo mark (original)
│   ├── bg-pattern.svg  Background graphic for the home page (original)
│   └── workplace.svg   Hero illustration (original)
├── docs/               Supporting documentation (see below)
└── README.md           This file
```

`docs/` is organised for the group's benefit; the filenames are our choice, not
an assessment requirement.

| File | What it is for |
|---|---|
| `release-checklist.md` | **Start here.** Every blocker, placeholder and remaining step |
| `decisions.md` | 13 source conflicts and interpretation choices, with the brief quoted |
| `requirements-matrix.md` | Every requirement mapped to code and evidence, against the 70-point rubric |
| `test-report.md` | What was actually tested, with results, including two defects found and fixed |
| `interview-guide.md` | Preparation for the Week 6 individual interview |
| `contributions.md` | Who did what - **empty, to be filled by the group** |
| `group-agreement-template.md` | Unsigned draft; submit before starting project work |
| `jira-backlog.csv` | 41 proposed issues (8 epics, 11 stories, 22 tasks) across 2 sprints |
| `project-workflow.md` | Sprint plan, ownership split, branch conventions |
| `references.md` | Asset origins and sources. No third-party code or assets are used |
| `ai-use.md` | Full generative AI disclosure |

---

## Previewing locally

The site is plain files. Double-clicking `index.html` works.

To test it the way GitHub Pages serves it - from a **subdirectory** - serve from
the parent folder, which is how the relative paths were verified:

```bash
cd ..
python -m http.server 8777
```

Then open `http://127.0.0.1:8777/applied-web-project-part1/index.html`.

---

## Verification status

| Check | Result |
|---|---|
| HTML5 validation, all four pages | **0 errors** (Nu Html Checker `vnu-jar` 26.9.16) |
| CSS validation | **0 errors** (W3C CSS Validator, profile CSS3) |
| Responsive at 320 / 375 / 768 / 1024 / 1440 | **No horizontal page scroll at any width** |
| Assessed float on `jobs.html` | `float: right`, measured **25.0%**, contained |
| Form boundary cases | **31 of 31** matched expectations |
| POST to the Mercury test script | **HTTP 200**, all 13 fields echoed correctly |
| Colour contrast | lowest measured pair **7.32:1** |
| JavaScript / frameworks / CDN | **none present** |

Two real defects were found by testing and fixed: an invalid `autocomplete` token,
and horizontal page overflow at 320px caused by the wide tables. Both are written
up in `docs/test-report.md`.

**Not verified:** screen reader testing, Firefox and Safari, the unit's own
`WebValidator.jar` (it cannot run on JDK 21), and the Accessibility Guideline PDF
(not available). No accessibility score is claimed anywhere.

---

## Known limitations

These are deliberate and documented, not bugs to be quietly fixed:

- The date of birth field checks **format, not the calendar** - `31/02/2000`
  passes. (`decisions.md` D-06)
- Names accept **only A-Z and a-z**, so `Anne-Marie` and `O'Brien` are rejected.
  That is the brief's rule, implemented literally. (D-05)
- The search box **navigates, it does not filter**. (D-08)
- The skills checkboxes require **all five** to be ticked, which is the literal
  reading of the brief and needs tutor approval. (D-04)

---

## Replacing placeholders

Two searches find everything:

```bash
grep -rn 'class="tbd"' about.html     # member details, quotes, fun facts
grep -rn 'class="pending"' *.html     # Jira, GitHub and Pages URLs
```

`class="tbd"` must return **nothing** before you submit. `class="pending"` should
return exactly **one** hit per page - the Jira board, which does not exist yet.
Full instructions per placeholder are in `docs/release-checklist.md` section 3.

---

## Deployment

**Done.** The site is pushed to `main` and served by GitHub Pages from the
repository root.

| Item | Value |
|---|---|
| Repository | https://github.com/dangminh232006/Web-Project-Group-3 |
| Live site | https://dangminh232006.github.io/Web-Project-Group-3/ |
| Branch and path | `main`, root (`/`) |
| Verified | All four pages, `styles.css` and all three SVG assets return HTTP 200 with correct content types |

Redeploy is automatic: push to `main` and Pages rebuilds in about 40 seconds.

**Still not done:** the Jira board does not exist. See `docs/release-checklist.md`
section 6.

## Packaging

For packaging, the ZIP must contain the four pages, `styles.css`, `images/` and
`docs/`, and must match the deployed site exactly.

---

## Constraints this project respects

- HTML5 and CSS3 only. No JavaScript, Bootstrap, Tailwind, React, Vue or jQuery.
- One external stylesheet, plus one small embedded block and one inline
  declaration per page, as the brief requires.
- All paths relative, so the site works from a repository subdirectory.
- No external requests at all - no web fonts, no CDN, no hotlinked images.
- Comments throughout, including the CSS header block the unit mandates.
- Generative AI and external sources acknowledged in code comments, per the unit
  requirements.
