# Release checklist

COS10026 Applied Web Project - Part 1. Last updated 2026-09-16.

**This project is not submission-ready.** Work top to bottom. Nothing below can
be ticked by the person who wrote this file - each item needs a fact, an asset, a
decision or an external action that only the group or the tutor can provide.

---

## 1. Release blockers - the site is incomplete without these

| # | Blocker | Where | Who resolves it |
|---|---|---|---|
| B-01 | **Allocated group code and industry unknown.** The site is a provisional digital-services draft. Industry alignment is currently **not met**. | all pages; `decisions.md` D-01 lists the blocks to rewrite | Group, from the tutor |
| B-02 | **Group photograph missing.** One photo of the whole group, under 300KB. | `about.html` `#group-photo` | Group |
| B-03 | **Member names and student IDs missing.** | `about.html` `dl#contributions`, `#fun-facts` | Each member |
| B-04 | **Member quotes and English translations missing.** Each member supplies a quote in their own first language. Native English speakers pick a quote in another language they like. | `about.html` `.quote` | Each member individually |
| B-05 | **Contribution records missing.** Each member must own at least one page and its CSS. | `about.html`, `contributions.md` | Group, together |
| B-06 | **Fun facts missing**, each approved by the person it describes. | `about.html` `#fun-facts` | Each member |
| B-07 | **Team name, class day/time, tutor name missing.** | `about.html` `#class-details` | Group |
| B-08 | **Jira board contents unverified.** The board exists (https://group3-cos10026.atlassian.net/browse/SAM1) and is linked in the footer, but it could not be inspected from this workspace. Confirm it holds epics, stories, tasks and **two sprints**, and that the **tutor has access**. | board itself | Group |
| ~~B-09~~ | ~~GitHub repository does not exist.~~ **DONE** - https://github.com/dangminh232006/Web-Project-Group-3 | footer, all 4 pages | - |
| ~~B-10~~ | ~~Site is not deployed to GitHub Pages.~~ **DONE** - https://dangminh232006.github.io/Web-Project-Group-3/ | footer, all 4 pages | - |
| ~~B-11~~ | ~~Contact email is a placeholder.~~ **DONE** - now `105716425@student.swin.edu.au`. Note this address is now **publicly visible** on the live site. | footer, all 4 pages | - |

---

## 2. Tutor decisions needed - do not guess these

| # | Question | Reference |
|---|---|---|
| T-01 | **Which due date applies?** The requirements document says Monday Week 7, 20 April 2026, 11:59pm. Canvas says 2 Nov, 3:59am, available until 9 Nov. The two do not agree. | `decisions.md` D-02 |
| T-02 | **Skills checkboxes:** does "all fields required" mean every box must be ticked (what we built), or at least one (impossible in HTML alone)? | D-04 |
| T-03 | **Search box:** is a navigation-only prototype acceptable for Part 1? | D-08 |
| T-04 | **Form endpoint:** should `it000000` be replaced with the group's own Mercury account id? The path works as-is. | D-03 |
| T-05 | **Acknowledgement:** is a named Acknowledgement of Country required in addition to the inclusive employment statement? | D-07 |
| T-06 | **Name validation:** may we widen the alphabetic pattern to accept hyphens, apostrophes and accented letters? As specified it rejects `Anne-Marie`, `O'Brien` and `Nguyen` with diacritics. | D-05 |
| T-07 | **Week 6 interview:** what is the actual date and time of your tutorial? | D-12 |

---

## 3. Every placeholder, and how to replace it

### `about.html`

| Placeholder | Replace with |
|---|---|
| `[TEAM NAME]` | your registered team name |
| `[G01 to G06]` | your allocated group code |
| `[INDUSTRY FROM THE BRIEF]` | the matching industry name |
| `[DAY]`, `[START TIME to END TIME]` | your class day and time |
| `[TUTOR NAME]` | your tutor |
| `[Member N full name]` x4 | each member's full name |
| `[STUDENT ID N]` x4 | each member's student ID |
| `[which page(s) and which CSS sections this member wrote]` x4 | real ownership, matching the Git history |
| `[testing, Jira, assets, documentation]` x4 | real secondary contributions |
| `[Quote in member N's first language]` x4 | the member's own quote; **add a `lang` attribute**, for example `<p class="quote" lang="vi">` |
| `[translation of the quote above]` x4 | the English translation |
| `[Caption: the full team, left to right, with names]` | a real caption |
| Fun facts cells (16) | member-approved details |

Groups of three delete the fourth `<dt>`/`<dd>` block and the fourth table row.

**Search for `class="tbd"` to find every one of them.** When the page is finished
there should be **zero** matches, and the `.tbd` rule can be deleted from the
embedded `<style>` block along with the "Unfinished" warning note.

### All four pages

| Placeholder | Replace with |
|---|---|
| `Harbourline Digital` and the slogan | your industry-appropriate company name |

**No pending markers remain.** All four footer items - Jira, GitHub, GitHub Pages
and the contact email - are live links on every page. `grep -c 'class="pending"'`
returns 0 for all four pages, and the now-unused `.pending` CSS rules were
deleted rather than left as dead code.

### `styles.css`

| Placeholder | Replace with |
|---|---|
| `author: [PENDING - see docs/contributions.md ...]` | the names of the members who wrote the stylesheet |
| `last modified:` | the real date of the final edit |

---

## 4. Adding the group photo

1. Take **one** photo of the whole group together. Individual portraits do not
   satisfy the brief.
2. Resize to about 1200px wide.
3. Save as `images/team-photo.jpg`.
4. **Check the size:** `ls -l images/team-photo.jpg` - it must be under 300,000
   bytes. Aim under 250,000 as a buffer. If it is too large, re-export at a lower
   JPEG quality.
5. In `about.html`, replace the `<div class="photo-placeholder">` block with a
   real `img` element: `src="images/team-photo.jpg"`, a descriptive `alt`, and
   `width`/`height` matching the file. Write a real description, not "group photo".
6. Replace the `<figcaption>` placeholder with a real caption.
7. Delete the "How to finish this" note below the figure.
8. Reload and confirm the border still frames the image.

---

## 5. Final verification before packaging

Run these again after every placeholder is filled - filling text can break markup.

| # | Check | How |
|---|---|---|
| V-01 | HTML validates | `java -jar vnu.jar index.html jobs.html apply.html about.html` - expect no output and exit 0. Or upload each page to `validator.w3.org`. |
| V-02 | CSS validates | Upload `styles.css` to `jigsaw.w3.org/css-validator`, profile CSS3 - expect 0 errors |
| V-03 | No placeholders left | `grep -c 'class="tbd"' about.html` and `grep -c 'class="pending"' *.html` - both must be **0** |
| V-04 | Photo under 300KB | `ls -l images/team-photo.jpg` |
| V-05 | All links work | Click every nav link, every Apply link, the footer links and the skip link, on all four pages |
| V-06 | Form still works | Submit valid synthetic data; confirm the Mercury script echoes every field, including the leading zero in the postcode |
| V-07 | Responsive | Resize to 320, 375, 768, 1024, 1440. No sideways page scroll at any width. The jobs aside floats right only on the widest two. |
| V-08 | Keyboard only | Tab through every page without a mouse. The focus ring must always be visible and the skip link must come first. |
| V-09 | Screen reader pass | Run NVDA or VoiceOver over `apply.html` and `about.html`. **Not yet done.** |
| V-10 | Accessibility Guideline PDF | Download it from Canvas, read it, re-check all four pages against it. **Not yet done.** |

---

## 6. Deployment and submission

Steps 1, 2 and 4 are **done**. The rest are still outstanding.

| Done | Item |
|---|---|
| YES | Jira board linked in the footer: https://group3-cos10026.atlassian.net/browse/SAM1 (contents not verified) |
| YES | Repository created and code pushed to `main`: https://github.com/dangminh232006/Web-Project-Group-3 |
| YES | GitHub Pages enabled (branch `main`, root) and building: https://dangminh232006.github.io/Web-Project-Group-3/ |
| YES | GitHub and Pages URLs embedded in the footer of all four pages |
| PARTIAL | Jira board exists and is linked, but its contents and tutor access are unverified |

1. ~~Create the GitHub repository.~~ **Done.** But note: the first real commit was
   made by one account. **Each member must still commit their own page** under
   their own GitHub account, or the history will not evidence the "one page each"
   requirement (rubric G11).
2. ~~Enable GitHub Pages.~~ **Done.**
3. Open the live URL and re-run V-05 and V-07 **on the deployed site**, not just
   locally. Check the browser console for missing files.
4. ~~Put the Jira, GitHub and Pages URLs into the footer.~~ **Done** on all four
   pages. Pages redeploys automatically about 40 seconds after any push to `main`.
   **Open the Jira footer link while logged in** and confirm it lands on the
   project, then confirm the tutor can open it too.
5. Create the Jira project, import or hand-enter `jira-backlog.csv`, run the two
   sprints, and **share the board with your tutor**.
6. Submit the Group Agreement. It is due **before** project work begins and must
   not be backdated.
7. Build the ZIP. It must contain the four pages, `styles.css`, `images/` and
   `docs/`, and must match the deployed site exactly.
8. Submit the ZIP on Canvas, and paste the live site URL and the repository URL
   into the submission comment.
9. Each member: attend the Week 6 interview, and submit the individual Project
   Self Report and the Peer & Self Evaluation.

> Documentation in this folder is not evidence that any of the above happened.
> A backlog file is not a Jira board, and deployment instructions are not a
> deployed site.
