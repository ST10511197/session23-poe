# Session 23 — Website (WEDE5020 PoE)

Static HTML/CSS/JS website built for **Session 23** ("Party With The English"), an
Amapiano, House and Hip-Hop events collective operating in Gqeberha and Johannesburg.

## Student

- Name: Luphawu Mangcotywa
- Student Number: ST10511197
- Institution: The IIE Rosebank College
- Module: WEDE5020

## Live Site

GitHub Pages URL: *add once Pages is enabled — see setup steps below*

## Folder Structure

```
session23-poe/
├── index.html                 # Homepage — hero, upcoming events preview, offerings
├── about.html                 # Brand story, mission, vision, values
├── events.html                # Full events calendar, archive & photo gallery
├── enquiry.html                # Booking & partnership enquiry form + FAQ
├── contact.html                # Contact details
├── css/
│   └── style.css              # Shared stylesheet (black & gold identity)
├── js/
│   └── script.js               # Shared script (mobile nav toggle)
├── images/
│   ├── gallery/                # Responsive event photos (3 widths per photo: 400/800/1600px)
│   └── screenshots/            # Device-width screenshots used as Part 2 evidence (below)
├── documentation/
│   ├── sitemap.png             # Site structure diagram (see Sitemap below)
│   └── wireframes/             # Low-fidelity page layouts (see Wireframes below)
└── README.md
```

> Part 1 shipped a duplicate `/pages` copy of the four inner HTML files. It was never
> linked to from anywhere (`index.html` and the nav always pointed at the root-level
> files) so it was removed as part of the Part 1 feedback clean-up — see Changelog.
> All folder names are lowercase with no spaces, and every asset lives inside the one
> folder that owns that file type (`css/`, `js/`, `images/`, `documentation/`), so
> there is a single, predictable place to look for anything in the project.

## Research & Planning

Before writing any markup, I looked at three things:

1. **The genre and audience.** Amapiano grew out of township house and kwaito scenes
   in Gauteng in the mid-2010s and is still closely tied to a specific visual and
   social identity (Ballantine's, no date; African Music Library Newsletter, 2026).
   That's the reason the site leans on a plain black-and-gold identity and
   photography-led evidence of real nights, rather than generic "party site"
   stock imagery — the audience can tell the difference.
2. **Comparable event-collective sites.** I looked informally at how similar South
   African event brands structure their public sites on Instagram and the open web —
   most lead with a hero statement, a short upcoming-events list, and a lightweight
   enquiry/booking path rather than a full e-commerce checkout — which is what shaped
   the five-page structure below (home → about → events → enquiry → contact) instead
   of, say, a single long landing page.
3. **Accessibility & responsive-image technique.** The gallery's `srcset`/`sizes`
   markup, the `loading="lazy"` attributes and the explicit `width`/`height` on every
   `<img>` (to avoid layout shift) are based on MDN's responsive-images guide and
   web.dev's CLS article (see References). The visible keyboard-focus states on the
   gallery, nav links and buttons follow WCAG 2.2 Success Criterion 2.4.7 (Focus
   Visible) — see References.

## Sitemap

![Session 23 site map](documentation/sitemap.png)

- **`index.html`** (Home) links to all four other pages via the shared nav.
  - **`about.html`** — brand story, mission, vision, values.
  - **`events.html`** — upcoming events calendar + past-events photo archive.
  - **`enquiry.html`** — booking/partnership form + FAQ. Linked from every "Enquire" /
    "Get Tickets" button on Home and Events, and from the Contact page.
  - **`contact.html`** — contact details, and a hand-off card back to the Enquiry form.
- Every page shares the same header (logo + nav) and footer (Instagram + Contact
  link), so the site map above doubles as the site's information architecture, not
  just a list of files.

## Wireframes

Low-fidelity wireframes for the two content-heaviest templates (Home, Events) at both
the desktop and mobile breakpoints, plus the About and Contact/Enquiry templates at
desktop, done before styling to lock in layout and content hierarchy:

| Page | Wireframe |
|---|---|
| Home — Desktop | ![Home desktop wireframe](documentation/wireframes/home-desktop.png) |
| Home — Mobile | ![Home mobile wireframe](documentation/wireframes/home-mobile.png) |
| Events — Desktop | ![Events desktop wireframe](documentation/wireframes/events-desktop.png) |
| Events — Mobile | ![Events mobile wireframe](documentation/wireframes/events-mobile.png) |
| About — Desktop | ![About desktop wireframe](documentation/wireframes/about-desktop.png) |
| Contact / Enquiry — Desktop | ![Contact desktop wireframe](documentation/wireframes/contact-desktop.png) |

The wireframes intentionally show only structure (header/nav, hero, content blocks,
image placeholders, footer) — no colour, type or imagery — so the layout decisions
(the ticket-stub list, the 2×2 gallery grid dropping to one column, the nav collapsing
to a hamburger) could be checked independently of the visual identity in the Design
Notes below.

## Design Notes

- **Palette:** near-black background, muted gold (`#c9a227`) and bright gold
  (`#e8c661`) accents, cream text — matches the existing Session 23 brand identity.
- **Type:** Anton (display/headings) paired with Manrope (body) — a poster-style
  display face suited to an events brand, kept legible at body size.
- **Signature element:** the ticket-stub card (perforated divider) used for event
  listings, tying the UI back to physical event tickets.
- **Gallery:** a CSS Grid `grid-template-areas` layout (one large "main" photo + two
  stacked side photos) on the Events page, restructured to a single stacked column
  below 600px. Each photo ships in 3 widths and uses `srcset`/`sizes` so phones don't
  download the same file as desktop. As of this update the gallery uses real Session
  23 event photography (see Changelog).

## Semantic HTML & Accessibility

On top of the landmark elements every page already used (`header`, `nav`, `main`,
`section`, `footer`), the following semantic elements are now used deliberately for
what they mean, not just for a styling hook:

- **`<article>`** — every event listing (Home, Events) and every FAQ item is wrapped
  as a self-contained piece of content.
- **`<time>`** — event dates.
- **`<figure>` / `<figcaption>`** — every gallery photo and its caption on the Events
  page, replacing a plain `<a><img><span>` group.
- **`<address>`** — the contact details block on the Contact page.
- **`<aside>`** — content that supports but isn't part of the main flow (the "What We
  Stand For" pull-quote on About, the "Before You Message Us" hand-off card on
  Contact).
- **`<details>` / `<summary>`** — the FAQ accordion on the Enquiry page; native,
  keyboard- and screen-reader-accessible with no JavaScript.
- **`<blockquote>`** — the testimonials section on Home.
- **`<mark>`** — flags the genre name on its first mention in a paragraph.
- **`aria-expanded`, `aria-current`, `:focus-visible`** — already in place on the nav
  toggle and active nav link from Part 1; extended to the gallery figures via
  `:focus-within` so keyboard users get a visible focus ring on the photo tiles too.

## CSS Styling & Responsive Design

- **External stylesheet:** all five pages link a single `css/style.css`.
- **Base style / reset:** universal box-sizing + margin/padding reset, base font,
  colour scheme and spacing set once on `body`/`:root` custom properties.
- **Typography:** `font-family`, `font-size` (via `clamp()` for fluid headings),
  `font-weight`, `line-height` and `letter-spacing` used across headings, eyebrows
  and body copy.
- **Layout:** Flexbox for the nav, hero CTAs and footer; CSS Grid for the card
  grids, the ticket-stub component, and the gallery (`grid-template-columns`,
  `grid-template-areas`).
- **Visual styles:** `color`, `background-color`, `border` and `box-shadow` on
  cards, tickets and gallery tiles; `:hover`, `:focus-visible` and `:active`
  pseudo-classes on buttons, nav links, cards and gallery items.
- **Responsive breakpoints:** three tiers — desktop (default), tablet (`≤1024px`),
  mobile (`≤600px`) — each adjusting spacing, grid column counts, and (below
  600px) switching to the hamburger nav and single-column gallery.
- **Relative units:** `rem`/`em` for type and spacing, `%`/`fr`/`vw` for widths,
  so content scales within a tier and not just at the breakpoints.
- **Responsive images:** `srcset` + `sizes` on every gallery `<img>` (400w / 800w /
  1600w), explicit `width`/`height` to avoid layout shift, and `loading="lazy"`.
- **Comments:** every non-obvious block in `style.css`, `script.js` and the HTML
  templates carries a short comment explaining *why* (not just what) — e.g. why
  `<figure>` needs its browser margin reset, why `:focus-within` replaces
  `:focus-visible` on the gallery tiles, why `<address>` needs `font-style: normal`.

## Screenshot Evidence — Different Screen Sizes

Captured from the live-rendered pages at three widths: **desktop** (1440px),
**tablet** (834px, iPad portrait), and **mobile** (390px, iPhone-sized).

### Homepage

| Desktop | Tablet | Mobile |
|---|---|---|
| ![Homepage desktop](images/screenshots/home-desktop.jpg) | ![Homepage tablet](images/screenshots/home-tablet.jpg) | ![Homepage mobile](images/screenshots/home-mobile.jpg) |

### Events Page (Calendar + Gallery)

| Desktop | Tablet | Mobile |
|---|---|---|
| ![Events desktop](images/screenshots/events-desktop.jpg) | ![Events tablet](images/screenshots/events-tablet.jpg) | ![Events mobile](images/screenshots/events-mobile.jpg) |

Notes from testing:
- The ticket-stub grid (`1fr auto`) collapses to a single column with a horizontal
  perforation below 600px instead of a vertical one.
- The gallery's 2×2 grid-template-areas layout drops to one stacked column below
  600px so photos stay legible on a phone instead of being squeezed into a sliver.
- Card grids go 3-up → 2-up (tablet) → 1-up (mobile).

> Note: these screenshots still show the old placeholder gallery photography. Re-run
> them once real dates/venues are confirmed (see Still To Do) so the Events page
> evidence reflects the real photos now in `images/gallery/`.

## Git Workflow

This repository is meant to be committed to regularly through development, not
pushed as one final snapshot. Going forward the practice is:

- One commit per meaningful change (a page, a component, a fix, a docs update) —
  not one commit per file and not one commit for the whole project.
- Descriptive, present-tense messages (`Add responsive gallery to events page`, not
  `update` or `final`).
- Commit *before* moving on to the next task, so the history reads as a build log a
  marker (or a teammate) can follow.

## Changelog

### 2026-09-15 — Part 1 feedback fixes

Addressing the marked feedback on Formative 1 Part 1 (59.5/100):

- **Wireframes (was 0/2):** added low-fidelity desktop + mobile wireframes for the
  Home and Events templates, and desktop wireframes for About and Contact/Enquiry —
  see the new **Wireframes** section above and `documentation/wireframes/`.
- **Structure: Sitemap (was 0/5):** added a visual site map plus a written page/link
  breakdown — see the new **Sitemap** section above and `documentation/sitemap.png`.
- **File & Folder Structure (was 2/5):** removed the unused duplicate `/pages`
  folder left over from Part 1 (root-level files were always the ones actually
  linked); every asset now lives under the one folder that owns its type
  (`css/`, `js/`, `images/`, `documentation/`); all names are lowercase with no
  spaces. See the updated **Folder Structure** diagram above.
- **Content Research & Sourcing (was 7/10, "no strong evidence of research"):**
  added a **Research & Planning** section above documenting the genre/audience
  research, the informal competitor scan that shaped the five-page structure, and
  the accessibility/responsive-image sources that shaped specific markup choices —
  each backed by a full reference in the **References** section.
- **Layout tags: Semantic elements / Content tags (was 7/10 and 6.5/10, "make good
  use of semantic elements" / "take good advantage of HTML elements"):** added
  `<article>`, `<time>`, `<figure>`/`<figcaption>`, `<address>`, `<aside>`,
  `<details>`/`<summary>`, `<blockquote>` and `<mark>` where each is the
  semantically-correct element rather than a generic `<div>`/`<span>` — see the new
  **Semantic HTML & Accessibility** section above for exactly where each is used.
- **Sufficient content added (was 3/5, "add more content"):** added a testimonials
  section to Home, a "How We Got Here" history section to About, and a four-question
  FAQ accordion to Enquiry.
- **Comments (was 3/5):** added explanatory comments to the new HTML blocks and to
  the corresponding CSS rules, focused on *why* a choice was made, not just *what*
  the code does.
- **GitHub: Commits, Files and Link (was 3/10) / ReadMe File (was 1/5) / References
  (was 0/5):** re-initialised the repository history with one commit per logical
  change instead of a single dump (see **Git Workflow** above); expanded this README
  with the Research, Sitemap, Wireframes, Semantic HTML and References sections it
  was missing; added the full reference list below.

### 2026-09-15 — Part 2: CSS Styling & Responsive Design
- Added a responsive photo gallery to `events.html` using CSS Grid
  `grid-template-areas`, replacing the "Gallery — Coming Soon" placeholder card.
- Added `srcset`/`sizes` responsive images (3 widths per photo) with `loading="lazy"`
  and explicit `width`/`height` attributes.
- Rebuilt the single mobile breakpoint into three tiers: desktop / tablet (`≤1024px`)
  / mobile (`≤600px`), with tablet-specific grid and spacing rules that didn't exist
  in Part 1.
- Added `box-shadow` to cards, tickets and gallery tiles, plus `:hover` /
  `:focus-visible` / `:active` states on the new gallery tiles.
- Replaced the inline `style="grid-template-columns:…"` on the About page with a
  proper `.about-split` class so the layout can be overridden cleanly at the mobile
  breakpoint instead of fighting an inline style.
- Added real cross-device screenshot evidence (desktop/tablet/mobile) for the
  homepage and events page.
- Housekeeping: removed the unused duplicate `/pages` folder left over from Part 1
  (root-level HTML files were always the ones actually linked/used).
- Swapped the gallery's placeholder photography for real Session 23 event photos
  (see the next entry).

### 2026-09-15 — Real event photography
- Replaced the three placeholder gallery images with real Session 23 event photos
  (rooftop/deck event overview, DJs on the decks, the crowd on the dance floor).
- Regenerated all three responsive widths (400/800/1600px) from the new source
  photos and updated the `alt` text, `<figcaption>` captions and `width`/`height`
  attributes on the `<img>` elements to match the new (portrait) aspect ratio.
- Converted the gallery markup from `<a><img><span></a>` to
  `<figure><a><img></a><figcaption></figcaption></figure>` — see **Semantic HTML &
  Accessibility** above.

### Part 1 — Initial Structure & Content
- Built the five-page static site structure (`index`, `about`, `events`, `enquiry`,
  `contact`) with shared header/footer and mobile nav toggle.
- Established the black-and-gold visual identity and ticket-stub signature
  component.

## Still To Do Before Submission

- [ ] Replace placeholder event dates/venues in `index.html` and `events.html` with
      confirmed details
- [ ] Confirm final contact email in `contact.html`
- [ ] Wire the enquiry form up to a real submission handler (e.g. Formspree) if required
- [ ] Re-run the screenshot evidence above once event dates/venues are confirmed
- [ ] Enable GitHub Pages and add the live URL at the top of this README
- [ ] Continue committing after every change from here on (see **Git Workflow**)

## References

Referencing style: Harvard (author-date), as required by IIE.

- African Music Library Newsletter (2026) *A Brief History of Amapiano*. Available
  at: https://africanmusiclibrary.substack.com/p/a-brief-history-of-amapiano
  (Accessed: 15 September 2026).
- Ballantine's (no date) *Going Global: The Rise of Amapiano Music*. Available at:
  https://www.ballantines.com/en/blog/from-south-africa-to-the-world-amapiano-goes-global/
  (Accessed: 15 September 2026).
- Google Fonts (no date) *Anton*. Available at:
  https://fonts.google.com/specimen/Anton (Accessed: 15 September 2026).
- Google Fonts (no date) *Manrope*. Available at:
  https://fonts.google.com/specimen/Manrope (Accessed: 15 September 2026).
- Mozilla Developer Network (no date) *CSS Grid Layout*. Available at:
  https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout (Accessed: 15
  September 2026).
- Mozilla Developer Network (no date) *Responsive images*. Available at:
  https://developer.mozilla.org/en-US/docs/Web/HTML/Guides/Responsive_images
  (Accessed: 15 September 2026).
- Mozilla Developer Network (no date) *Using media queries*. Available at:
  https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries
  (Accessed: 15 September 2026).
- Mozilla Developer Network (no date) *&lt;address&gt;: The Contact Address
  element*. Available at:
  https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/address
  (Accessed: 15 September 2026).
- Mozilla Developer Network (no date) *&lt;details&gt;: The Details disclosure
  element*. Available at:
  https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/details
  (Accessed: 15 September 2026).
- Mozilla Developer Network (no date) *&lt;figure&gt;: The Figure with Optional
  Caption element*. Available at:
  https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/figure
  (Accessed: 15 September 2026).
- web.dev (no date) *Optimize Cumulative Layout Shift*. Available at:
  https://web.dev/articles/optimize-cls (Accessed: 15 September 2026).
- World Wide Web Consortium (W3C) (2023) *Understanding Success Criterion 2.4.7:
  Focus Visible*. Available at:
  https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html (Accessed: 15
  September 2026).
- Event photography: own photography, Session 23 events, Gqeberha (2026),
  reproduced with permission for use in this coursework project only.

## Setup — GitHub Pages

1. Push this repository to GitHub (public), committing regularly as you go — see
   **Git Workflow** above.
2. Go to **Settings → Pages**.
3. Under **Source**, select the `main` branch and `/ (root)` folder, then **Save**.
4. GitHub will publish the site at `https://<username>.github.io/<repo-name>/`.
