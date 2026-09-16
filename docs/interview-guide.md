# Interview preparation guide

COS10026, individual component of Applied Web Project Part 1.

> **Read this first.** This guide explains the code. It is **not** evidence that
> you understand it, and reciting it is not the same as understanding.
>
> The interview asks you to *explain and justify your code*, and a tutor can ask
> you to change something on the spot. The only preparation that actually works
> is opening your page, reading every line, and changing things until you can
> predict what will happen before you press refresh.
>
> If you cannot yet explain a section, that is useful information: go and rewrite
> that section yourself.

---

## 1. Practical drills - do these before the interview

Give yourself 30 minutes with the code and no notes.

| Drill | What it proves |
|---|---|
| Delete `<link rel="stylesheet">` from one page, reload, then put it back | You understand what the external stylesheet is doing |
| Change `.job__aside { width: 25% }` to `40%` and reload at desktop width | You can find and change the assessed float |
| Narrow the window to 320px and watch the aside stop floating | You understand the media query |
| Remove `required` from one field and try to submit empty | You understand constraint validation |
| Change the `pattern` on postcode to `[0-9]{3}` and try `0800` | You understand `pattern` |
| Add a fifth row to the fun facts table | You can edit a table without breaking it |
| Tab through the page with no mouse | You can demonstrate the accessibility features |
| Break something on purpose, run the validator, and read the error | You can use the validator, which is what the unit expects |

---

## 2. Page-by-page walkthrough

### `index.html` - Home

**Purpose:** introduce the company and route people to Jobs or Apply.

| Element | Where | Why it is there |
|---|---|---|
| `<a id="skip-link">` | first in `<body>` | Lets keyboard users jump past the nav. Hidden at `left: -9999px` until focused |
| `.brand` | `#site-header` | Logo, name and slogan - three separate brief requirements |
| `#home-hero` | `<main>` | Carries the **CSS background graphic** requirement via `background-image` |
| Process table | mid-page | Carries the **cell merging** requirement |
| `#site-search` | below the table | The search box and button |
| `#acknowledgement` | before the footer | The inclusion requirement |

**The table is the part most likely to be asked about.** It uses both merge types:

```html
<th scope="col" rowspan="2">Phase</th>      <!-- spans both header rows -->
<th scope="colgroup" colspan="2">What to expect</th>  <!-- spans two columns -->
...
<th scope="rowgroup" rowspan="2">Apply</th> <!-- one phase, two stages -->
```

- `rowspan="2"` on *Phase* and *Stage*: those headers have no sub-heading, so they
  occupy both header rows.
- `colspan="2"` on *What to expect*: it sits above two columns that each have
  their own heading in the second row.
- `scope` tells a screen reader which header governs which cell. Once cells are
  merged, that is no longer obvious from position alone - which is exactly why
  `scope` matters here and not in a simple table.

**Likely question: "why is the search box not a real search?"**
Because filtering needs either JavaScript or server-side code, and the brief
forbids JavaScript in Part 1. Submitting the form navigates to `jobs.html`. The
note under the field says so on the page. A query string in the address bar is
not filtering.

### `jobs.html` - Job descriptions

**The assessed float.** Base rule, which is what mobile gets:

```css
.job__aside { border: 2px solid var(--c-brand); padding: 1rem; margin: 0 0 1.25rem; width: auto; }
```

Then from 1024px up:

```css
@media screen and (min-width: 64em) {
  .job__aside { float: right; width: 25%; margin: 0 0 1rem 1.5rem; }
}
```

**Be ready for: "why is the float in the media query instead of being removed in
one?"** This is mobile-first. The narrow layout is the default, and the float is
*added* for wide screens rather than added then undone. Same result, one rule
instead of two, and the small-screen case needs no override at all.

**Be ready for: "what stops the float escaping the card?"**
`.job { display: flow-root }`. A floated element is taken out of normal flow, so
its parent would otherwise collapse and the float would overhang the next
section. `flow-root` creates a new block formatting context that contains it. The
older technique is a clearfix with `::after { content: ""; display: table; clear: both }`
- know both, and say why you chose the modern one.

**Where the required lists are:** the `<ol>` is the numbered "How to apply" steps,
because those are genuinely sequential. The `<ul>`s are responsibilities and
requirements, where order does not matter.

### `apply.html` - The form

This page carries the most marks per line. Know these five things cold.

**1. Why the date of birth is `type="text"` and not `type="date"`.**
`type="date"` submits `yyyy-mm-dd`. The brief specifies `dd/mm/yyyy`. Using the
date picker would change the submitted format, so a text input with a pattern was
used instead.

**2. What the date pattern can and cannot do.**

```
(0[1-9]|[12][0-9]|3[01])/(0[1-9]|1[0-2])/(19|20)[0-9]{2}
```

Reading it left to right: day is 01-09, 10-29 or 30-31; month is 01-09 or 10-12;
year starts 19 or 20 then any two digits.

It checks **shape and range**, not the calendar. `31/02/2000` passes. So does
`29/02/2001`, which is not a real date. Say this plainly if asked - it is a known
limitation, recorded in `decisions.md` D-06, and fixing it needs server-side code
or JavaScript.

**3. Why postcode and phone are `type="text"` and not `type="number"`.**
`type="number"` treats the value as a number, so `0800` becomes `800` and the
leading zero is lost. Australian postcodes such as Darwin's `0800` and phone
numbers such as `0390001234` need that zero. `inputmode="numeric"` still brings
up the numeric keypad on a phone, without the numeric value semantics.

**4. The skills checkboxes, and why the page says what it says.**
The brief says all fields except the textarea are required. Putting `required` on
each checkbox makes **every** box compulsory. HTML has no way to express "at
least one of this group" - there is no attribute for it, and JavaScript is
forbidden. So the literal reading was implemented and the consequence was written
on the page. If the tutor says the intent was "at least one", the honest answer is
that it cannot be done in HTML alone and would move to PHP in Part 2.

**5. Why the name is `skills[]` and not `skills`.**
Tested against the unit's own Mercury echo script: with `name="skills"` only the
**last** ticked box arrives and the other four are silently discarded. With
`name="skills[]"` all five arrive. This is a good thing to raise unprompted - it
shows you tested rather than assumed.

**The Grid layout.** `#application-form { display: grid }`, one column by default,
two from 40em. Fieldsets and wide fields use `grid-column: 1 / -1` to span the
full width. Individual fields use `display: flex; flex-direction: column` so the
label, control and hint stack.

### `about.html` - Team page

| Requirement | How it is met |
|---|---|
| Nested list | `#class-details` - a `<ul>` whose `<li>` contains another `<ul>` |
| Definition list | `dl#contributions` - `<dt>` per member, several `<dd>` per member |
| Styled student IDs | `.student-id` - monospace, letter-spaced, white on `#0d4f5c` |
| Bordered figure | `#group-photo { border: 4px solid #0d4f5c }` |
| Hex colours in the table | `#0d4f5c`, `#f2f7f8`, `#dbeceb`, `#08333c` |
| Hover effect | `#fun-facts tbody tr:hover` |

**Be ready for: "why is a `<dl>` right here and not a `<ul>`?"**
Because the content is genuinely name-and-value pairs: the member is the term and
their contribution, quote and translation are descriptions of it. A `<ul>` would
lose that relationship.

---

## 3. Questions about the whole site

**"Show me where the shared navigation is and how the current page is marked."**
`#site-nav` in the header of all four pages, same four links in the same order.
The current page carries `aria-current="page"`, and CSS targets that attribute:
`#site-nav a[aria-current="page"]`. The styling and the accessible state come from
the same attribute, so they cannot drift apart.

**"How many places is CSS written, and why?"**
Three, and the brief requires all three. Almost everything is in `styles.css`.
Each page has one small `<style>` block for rules only that page uses, and one
`style` attribute on a single element where the value is genuinely one-off. The
brief warns that overusing inline and embedded CSS loses marks, so there is
exactly one of each per page.

**"Name some different CSS selectors you used and why."**
Have three ready:
- `#site-nav a[aria-current="page"]` - an attribute selector, so no extra class is
  needed on the current link.
- `.responsibilities > li` - a child combinator, so only direct items are spaced.
- `#fun-facts tbody tr:nth-child(even)` - a structural pseudo-class for zebra
  striping without marking up every second row.

**"What makes this accessible?"**
Pick concrete things, not adjectives: semantic landmarks; one `h1` per page with
no skipped levels; a skip link; a visible 3px focus ring via `:focus-visible`;
every form control has a real `<label>`, with format hints wired by
`aria-describedby`; tables have captions and `scope`; contrast is at least 7.3:1
everywhere; the layout reflows to 320px with no sideways scrolling; and
`prefers-reduced-motion` is respected.

**"Why does the wide table sit inside a `<div>` with `tabindex="0"`?"**
A good question to be honest about. Testing at 320px showed the four-column tables
forcing the **whole page** to scroll sideways, which breaks WCAG reflow. The fix
puts the table in its own `overflow-x: auto` region. Once you create a scrollable
region you must make it keyboard reachable, which is what `tabindex="0"` does,
and it has a visible focus outline.

**"What is not finished?"**
Answer honestly and specifically: the group code and industry are not allocated,
so the content is a provisional digital-services draft; the group photo, member
details and quotes are placeholders; the Jira board and GitHub deployment do not
exist; and the Accessibility Guideline PDF has not been reviewed. A clear-eyed
answer here is worth more than pretending.

---

## 4. If you are asked to change something live

Stay calm and narrate what you are doing.

| Likely request | Where to go |
|---|---|
| "Make the aside 30% wide" | `styles.css` section 8, the `min-width: 64em` block |
| "Add a third job" | Copy a `<section class="job">` block in `jobs.html`, change the heading, reference and details |
| "Make the postcode accept 5 digits" | `apply.html`, `pattern="[0-9]{4}"` and the two length attributes |
| "Change the brand colour" | `styles.css` section 1, `--c-brand` in `:root` - one change, whole site |
| "Add a row to the fun facts table" | `about.html` `#fun-facts tbody` |
| "Make this heading bigger" | `styles.css` section 1, then check the 40em media query which overrides `h1` |

Two habits that read well: say *why* before you type, and reload and check rather
than assuming it worked.
