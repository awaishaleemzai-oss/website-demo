# Sab Seekhein — Free Education Directory for Pakistani Students

A static, no-backend website listing genuinely free education resources for
Pakistani students, organised by stage: Primary → Middle → Secondary →
Intermediate → Higher Education, plus a Scholarships page.

No subscriptions, logins, build tools, or server are required to run or use
this site — it's plain HTML, CSS, and JavaScript.

## How to open it

Just open `index.html` in a browser. Everything works locally.

For the search/filter features to work smoothly with no console warnings,
it's best to serve the folder instead of double-clicking the file. Any of
these work from inside this folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

or, with Node installed:

```bash
npx serve .
```

## How to publish it for free

This is a static site, so any free static host works:

- **GitHub Pages**: push this folder to a repo, enable Pages in repo settings.
- **Netlify / Vercel / Cloudflare Pages**: drag-and-drop the folder in their
  dashboard, or connect a git repo. All have free tiers sufficient for this.

No environment variables, database, or backend setup needed.

## File structure

```
index.html          Homepage — hero, stats, stage navigator, stage previews
stage.html           Single stage page, reads ?id=primary|middle|secondary|intermediate|higher
resources.html        Full searchable directory of every resource, with stage filter chips
scholarships.html    Scholarship & financial aid listings
about.html           About / why this site exists
contribute.html       "Suggest a resource" form (opens a pre-filled email, no server)
404.html             Not-found page

css/style.css        All styling — one file, organised by section, with design tokens at the top

js/data.js           **The content.** All resources, scholarships, and support links live here.
js/main.js           Shared header/footer injection + mobile nav behaviour
js/cards.js          Turns resource objects into the card HTML used across pages
```

## How to add or edit a resource

Everything you'll want to change day-to-day lives in **`js/data.js`**.
You don't need to touch any HTML or CSS to add a resource.

1. Open `js/data.js`.
2. Find the right stage inside `SITE_DATA.stages` (e.g. `id: "primary"`).
3. Copy an existing object inside that stage's `resources` array and edit:

```js
{
  name: "Resource Name",
  type: "App + Web",            // short category label shown under the name
  cost: "Free",                  // shown as a pill, e.g. "Free", "Free to audit"
  desc: "One or two sentences on what it teaches and why it's worth using.",
  link: "https://example.com",
  tags: ["Math", "Science"]      // short keyword chips, used by search too
}
```

4. Save the file — no build step. Refresh the page and it appears everywhere
   relevant (homepage preview, stage page, and the all-resources directory).

To add a new **stage** entirely, copy a whole stage object (with its own
`id`, `rung`, `label`, `gradeRange`, `tagline`, `color`, and `resources`)
and add it to the `stages` array — it will automatically appear in every
nav menu, the path navigator, and the footer link list, since those are all
generated from this same array.

To edit **scholarships**, do the same inside `SITE_DATA.scholarships`.

## Notes on accuracy

Every resource currently listed was verified as free-to-access at the time
this site was built (mid-2026). Free programs occasionally change pricing,
shut down, or get replaced — it's worth periodically re-checking links,
especially government partnership programs (HEC–Coursera, Cisco/MOFEPT)
which sometimes run in time-limited cohorts.

## Design notes

- Palette, type pairing (Lora for display, Inter for body, JetBrains Mono for
  small labels), and the "education ladder" motif are explained inline as
  CSS custom properties at the top of `css/style.css`.
- The site respects `prefers-reduced-motion` and has visible keyboard focus
  states throughout.
- No external JS frameworks or build tools — easy to host anywhere, easy to
  read and modify even for a beginner.
