# Release checklist

COS10026 Applied Web Project - Part 1, Group 3. Checked 23 October 2026.
This is the canonical submission checklist; Jira tracks the work and its evidence.

**Deadline:** 1 November 2026, 23:59 Vietnam time (2 November, 03:59 Melbourne time),
as displayed by the current group and individual Canvas assignments.

## 1. Group requirements

| ID | Status | Requirement and evidence | Owner / follow-up |
|---|---|---|---|
| B-01 | Complete | Class: Wednesday, 09:00-12:00, Thomas Harrison, recorded in `about.html` | Group-confirmed details |
| B-02 | Complete | All four names and student IDs appear in `about.html` | Four members |
| B-03 | Complete | Each member has a page and stylesheet, supported by actual Git authorship | `contributions.md` |
| B-04 | Complete | All four Vietnamese quotes and English translations appear with `lang="vi"` | `about.html` |
| B-05 | Open | Fun-facts table is styled, but three members still have 12 placeholder cells | Lan, Thang and Nhat Minh; WWTP-39 |
| B-06 | Open | Two supplied member portraits are used temporarily. Separate portraits do not fulfil the full-group photograph requirement | Group; WWTP-39 |
| B-07 | Complete | The old Before submission box is absent from the About page | `about.html` |
| B-08 | Partial | Jira has 8 epics, 11 stories, 22 tasks and two Part 1 sprints. Tutor access has not been verified | WWTP-45 |
| B-09 | Complete for audited code revision | Live files matched `23e4809`, and updated stylesheet-version links in `32a2b06` are published; all four skip links and both portraits were verified live | WWTP-44 records the deployment run and final verified commit |
| B-10 | Partial | Bui Dang Minh's Canvas Group Agreement shows Submitted, attempt 1, `Group3_GroupAgreement.docx`. Other members' submissions are unverified | Each member; WWTP-27 In Progress |
| B-11 | Unmet | Required in-code GenAI acknowledgements are absent. The owner has explicitly chosen to keep source files without comments | Documentation does not replace this requirement |
| B-12 | Unmet | Required explanatory CSS comments and external-source acknowledgements are absent | Source records in `references.md` do not meet an in-code requirement |
| B-13 | Interpretation pending | Only the HTML and CSS skill checkbox is required; other skills remain optional | Confirm interpretation with tutor; `decisions.md` D-04 |
| B-14 | Partial | Fresh HTML/CSS validation passed. Published skip links and keyboard controls passed; guideline/contrast review is complete. Fresh responsive widths and screen-reader coverage remain unverified | `test-report.md`; WWTP-43 Done, WWTP-42 In Progress |
| B-15 | Not submitted | Canvas group submission shows attempt 0. The release archive is generated from the final committed revision; its commit and verification are recorded in WWTP-46 | WWTP-25 and WWTP-46 In Progress until a Canvas receipt exists |

The fun-fact placeholders can be located with:

```bash
rg -n 'class="placeholder"' about.html
```

A clean search alone does not prove the group photograph or personal facts are authentic.

## 2. Individual submission and participation

| Item | Verified status / next action |
|---|---|
| Self-report | Word and PDF exist; keep their GitHub screenshots and counts aligned with the final repository history |
| Contribution evidence | Actual authored commits, merged page work and two original group-channel screenshots are available |
| Participation channel | The report uses Zalo at the student's request. The rubric names Discord; acceptance of Zalo evidence has not been confirmed |
| Week 6 interview | Bui Dang Minh confirmed on 23 October that the interview was completed in class. No grade or exact interview date is inferred; other members' attendance is not verified. WWTP-47 remains In Progress for the group |
| Peer and Self Evaluation | Canvas attempt 0. SPARKPLUS reports that the unit is not ready for the Student role; completion is blocked until the unit is enabled |
| Individual Canvas submission | Attempt 0. Upload Word or PDF directly, not a ZIP, before the deadline |

## 3. Final packaging and hand-off

1. Obtain the real group photograph and the remaining members' fun facts, then revalidate affected pages.
2. Confirm tutor access to Jira and resolve the skills-checkbox and Zalo-evidence interpretations.
3. Recheck changed live pages after the final commit and successful Pages deployment. Keep remaining
   limitations visible; do not turn open items into Done without evidence.
4. Rebuild `applied-web-project-part1.zip` from the final committed revision using `git archive`.
   Check that it includes all four HTML pages, five CSS files and every referenced image, and that its
   contents match that revision. Building a ZIP is not a Canvas submission.
5. Refresh report screenshots, commit counts and PDF after the final Git commit. Check image clarity,
   headings, page numbers, contents, captions and Word/PDF text consistency.
6. The student uploads the group ZIP with the live-site and repository links, then uploads the
   individual Word/PDF. Check the Canvas receipt for each; attempt 0 must not be reported as submitted.
7. Complete the peer evaluation when SPARKPLUS is available. Minh has confirmed completing the
   interview; each other member must confirm their own interview status.
