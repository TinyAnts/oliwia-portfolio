# Handoff: oliwiakonieczna.info (Oliwia's UX/product portfolio)

Read this first. It is written for whoever picks this project up next, human or AI,
on any account.

## What this is

The personal portfolio of **Oliwia Konieczna**, a CSPO-certified product and UX/UI
designer. It presents her case studies to recruiters and hiring managers. This is
her main professional site and the most important one in the family.

- **Live:** https://oliwiakonieczna.info
- **Repo:** `TinyAnts/oliwia-portfolio`, production branch `main`
- **Hosting:** Cloudflare Pages, auto-deploys on push to `main`

## Stack: plain static HTML, no build step

This is the one site in the family with **no framework and no build**. It is a
single `index.html` with all CSS inline in two `<style>` blocks, plus `403.html`,
`404.html`, and an `assets/` folder. Cloudflare Pages serves the repo root as-is.

Cloudflare build settings: framework preset **None**, build command **empty**,
output directory **empty** (or `/`). Do not add a build step.

```
index.html          the entire site (~38 KB)
404.html            branded not-found page (Pages serves this automatically)
403.html            branded forbidden page (not auto-triggered on a static site)
assets/
  case-01..05.webp  case study cover images, 1448x1086
  case-01..05.pdf   the full case study PDFs that the cards link to
  hero-photo.webp   mirrored crop of the portrait used in the hero
  portrait.webp     portrait used in the About section
  og.png            social share card
  favicon.svg
```

To work on it: clone the repo, edit `index.html`, serve the folder locally
(`python3 -m http.server`), screenshot, then commit and push.

Note: opening the downloaded `index.html` on its own, outside the repo folder,
shows broken images. That is expected, it needs its sibling `assets/` folder.

## The two `<style>` blocks

The first `<style>` block is the original editorial design (cream and burgundy).
The second block, right after it, is the **warm override** that defines the current
look and wins on every conflicting property. When changing colors or card styling,
edit the second block. The palette:

- background `#fff7f1` to `#fff4ec`, cards white
- accent coral `#e85d45`, deeper coral for text `#b64a33`, gradient partner `#f09e5e`
- ink `#33211c`, soft `#5f4a42`, muted `#96786c`, rules `#f4dccd`
- Fonts: Fraunces (serif, headings and accents) and Inter (body)

Visual signature: white rounded cards with a coral-to-amber gradient bar across the
top, pill-shaped section labels, soft coral-tinted shadows.

## Hero animation

The `h1` is wrapped in `.h1-reveal`, which animates a `clip-path` so the headline
looks like it is being written from left to right. An inline SVG under the word
"direction." draws itself using `stroke-dashoffset`. The intro paragraph and meta
row fade in after, on delays timed to follow the headline. All of it is disabled
under `prefers-reduced-motion`. If you retime the headline, retime the delays on
`.hero .lede` and `.hero .meta` to match.

The hero photo sits in a coral gradient frame (`.grad-frame`) with two floating
badge pills. There used to be a "Selected work" index card there instead; the case
studies are still reachable through the Work nav link and by scrolling.

## Case studies

Five case studies, numbered 01 to 05 in the copy, in this order:

1. COP homepage redesign (Hitachi Energy) -> `case-01.pdf`
2. Installed Base structure (Hitachi Energy) -> `case-02.pdf`
3. Glow, AI contingency analysis -> `case-05.pdf`
4. CASCADE for satellite operators (Okapi:Orbits) -> `case-03.pdf`
5. Space weather widget (Okapi:Orbits) -> `case-04.pdf`

**The display numbers do not match the file numbers.** Glow was added last, so it
got `case-05.*` files but sits third on the page. Each card also has an anchor id
(`#case-cop`, `#case-ib`, `#case-glow`, `#case-cascade`, `#case-widget`). Check the
anchor and the file path together when editing a card.

Case study PDFs are large. The Glow PDF was compressed from 11.6 MB to 1 MB with
ghostscript (`-dPDFSETTINGS=/ebook -dColorImageResolution=130`) with no visible
quality loss. Do the same for any new one rather than committing a raw export.

## Voice

Written in the first person, past tense, plainly. She says what the problem was in
human terms, then what she did, without buzzword stacking. Example of the register:
"I owned this one alone, from the first interviews to the shipped design."

Do not turn these back into fragment lists. Do not add em-dashes.

## Watch out for

- `.gitignore` excludes `_deploy/` and four large PDFs at the repo root. Leave it.
- The three testimonials are real, from named colleagues on LinkedIn. Do not edit
  their wording.
- Contact email on the site: `oliwiaakonieczna@gmail.com` (note the double `a`).

## House rules (apply to every site in this family)

These are the owner's standing preferences. Breaking them means redoing work.

1. **Never use em-dashes or en-dashes (the long dash characters) in site copy.**
   The owner considers them a tell that text was written by AI. Use commas,
   colons, semicolons, or the middot separator instead. Check with a search for
   the long dash characters before shipping.
2. **No invented testimonials, reviews, or endorsements presented as real.**
   Placeholder social proof stays behind a flag that is off in production.
3. **Free tiers only.** No paid subscriptions, no Stripe, no payment processors,
   nothing that would require registering a business.
4. **Write like a person.** Short punchy fragments stacked together read as
   machine-written. Prefer plain sentences in the first person.
5. **Preview before shipping.** Build, screenshot, and show the owner a preview.
   The owner reviews visually and gives precise feedback.
6. **Forms and interactive elements must stay accessible** (labels, focus states,
   reduced-motion fallbacks for animations).

## How deployment works

Every site follows the same path:

```
git push  ->  GitHub (TinyAnts/<repo>)  ->  Cloudflare Pages auto-build  ->  live domain
```

Cloudflare Pages watches the production branch of the GitHub repo and rebuilds on
every push. Nothing is uploaded by hand. Cloudflare account id:
`3869409b5f0d6bec2fa88ebf6106b5f1`.

If a push lands on GitHub but the site does not change, the Pages project has lost
its Git connection. Fix it at Cloudflare dashboard -> Workers & Pages -> the project
-> Settings -> Build -> Git repository -> Connect. If the repo is missing from the
dropdown, grant the Cloudflare Pages GitHub App access to it at
github.com/settings/installations. This has happened before on this account.

Custom domains are managed in the Pages project under Custom domains. DNS is
already on Cloudflare nameservers, so adding a subdomain there creates the DNS
record automatically. Give it a few minutes and expect browser/ISP DNS caching to
lag; testing in incognito does not bypass an OS-level DNS cache.

## The other sites in this family

| Repo | Live at | Stack |
|---|---|---|
| `TinyAnts/oliwia-portfolio` | oliwiakonieczna.info | static HTML, no build |
| `TinyAnts/oliwia-from-poland` | poland.oliwiakonieczna.info | Vite + React + TS |
| `TinyAnts/oliwia-yoga` | yoga.oliwiakonieczna.info | Vite + React + TS |
| `TinyAnts/career-copilot-360` | aivet.work | Vite + React + TS |
| `TinyAnts/raj-portfolio` | raj.aivet.work | Vite + React + TS |
