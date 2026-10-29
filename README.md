# Session 23 — Website (WEDE5020 PoE, Part 3)

Static HTML/CSS/JS website built for **Session 23** ("Party With The English"), an
Amapiano, House and Hip-Hop events collective operating in Gqeberha and Johannesburg.

## Student

- Name: Luphawu Mangcotywa
- Student Number: ST10511197
- Institution: The IIE Rosebank College
- Module: WEDE5020

## Live Site

GitHub Pages URL: `https://YOUR-USERNAME.github.io/session23-poe/` *(replace `YOUR-USERNAME` — see **Deployment** below)*
GitHub repository: *add the repository link here*

## Folder Structure

```
session23-poe/
├── index.html                 # Homepage — hero, upcoming events preview, offerings
├── about.html                 # Brand story, mission, vision, values
├── events.html                # Full events calendar, archive & photo gallery
├── enquiry.html               # Services list, enquiry form (cost + availability response), FAQ accordion
├── contact.html               # Contact details, contact form (compiles an email), map
├── 404.html                   # Custom "page not found" page
├── robots.txt                 # Crawler instructions (Part 3 SEO)
├── sitemap.xml                # Page list for search engines (Part 3 SEO)
├── css/
│   ├── style.css              # Shared stylesheet (black & gold identity)
│   └── vendor/                # Leaflet CSS + marker images (self-hosted)
├── js/
│   ├── data.js                # Events, services, pricing rules (single source of truth)
│   ├── script.js              # Nav toggle, DOM helper, scroll-reveal animation
│   ├── interactive.js         # jQuery accordion, tabs, modal + gallery lightbox
│   ├── events.js              # Dynamic event list: search, filter, sort
│   ├── services.js            # Dynamic services list
│   ├── map.js                 # Leaflet map + nearest-city geolocation
│   ├── forms.js               # Validation, enquiry AJAX submit, contact email builder
│   └── vendor/                # jQuery 3.7.1 + Leaflet 1.9.4 (self-hosted)
├── images/
│   ├── favicon.svg
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

## Part 3 — Enhancing Functionality and SEO

### 1. Interactive elements

| Requirement | Where | How |
|---|---|---|
| Accordion (jQuery) | `enquiry.html` FAQ | `js/interactive.js` — buttons with `aria-expanded`/`aria-controls`, `slideDown`/`slideUp`, one panel open at a time, arrow/Home/End keyboard support |
| Tabs (jQuery) | `events.html` (Upcoming / Archive / Map) | `role="tablist"`, arrow-key navigation, `fadeIn`, deep links such as `events.html#archive` |
| Modal | Events page "Details" button | Native `<dialog>` built in JS (`showModal()` gives the focus trap and Esc-to-close); closing returns focus to the button |
| Interactive map | Events page (Map tab) and `contact.html` | Leaflet + OpenStreetMap tiles, a marker per city (Gqeberha, Johannesburg) with a popup listing that city's events, plus a "Find my nearest city" button using the Geolocation API (only asks permission when clicked) |
| Animations & transitions | All pages | CSS keyframes for the hero and modals, scroll-reveal using `IntersectionObserver` + CSS transitions, jQuery fade/slide effects; everything switches off under `prefers-reduced-motion` |
| Advanced DOM manipulation | `js/script.js`, `events.js`, `forms.js`, `interactive.js` | A safe `el()` node builder (text via `createTextNode`, never `innerHTML`), event delegation, `<mark>` search-highlighting by splitting text nodes, dynamically created dialogs/result cards, live character counter, runtime `min`/`max` on the date picker, toggling `required` per service |
| Gallery with lightbox | Events page (Archive tab) | Click or press Enter on a photo to open the 1600px version in a modal, with previous/next buttons, arrow keys, Esc, "n of 3" caption and alt text; without JavaScript the link opens the image normally |

### 2. Dynamic content

- **Events list** (`js/data.js` → `js/events.js`): events are loaded from a data array and rendered as ticket-stub cards. A search box (debounced), City and Genre filters and a Sort control (soonest, A–Z, Z–A, city) update the list live, with a "no results" state and an `aria-live` result count. A `<noscript>` list keeps the content available to crawlers and no-JS visitors.
- **Services list** (`js/services.js`): the five service cards on the Enquiry page are built from the same data, and the form's Enquiry Type dropdown is filled from it, so they can never disagree.
- Changing an event, service or price means editing `js/data.js` in one place.

### 3. Search Engine Optimisation

**3.1 On-page SEO**

| Technique | What was done |
|---|---|
| Keyword research | Targets were chosen from how the audience searches: *genre + place* ("Amapiano events Gqeberha", "House music events Johannesburg"), *brand* ("Session 23", "Party With The English") and *action* ("book Amapiano event", "brand partnership"). Each page owns a different cluster (table below) so the pages do not compete with one another. Both "Gqeberha" and the older "Port Elizabeth" are used in body copy because people still search both. |
| Title tags | Unique, under 65 characters, keyword first: e.g. `Upcoming Amapiano & House Events \| Session 23` |
| Meta descriptions | Unique per page, 110–145 characters, written as a call to action, plus `keywords`, `author`, `robots` and `theme-color` meta tags |
| Header tags | Exactly one `<h1>` per page, `<h2>` for sections, `<h3>` for cards/items; no skipped levels |
| Image optimisation | Descriptive file names (`gallery-nirvana-800.jpg`), meaningful `alt` text on every image, `srcset`/`sizes` so phones download small files, `loading="lazy"`, explicit `width`/`height`, and the 1600px JPEGs re-encoded as progressive JPEG at quality 80 |
| URL structure | Flat, lowercase, hyphen-free single-word URLs (`/events.html`, `/enquiry.html`); no query strings are needed to reach any page. Event links use `enquiry.html?event=...` only to pre-fill the form |
| Internal linking | Every page links to the others in the body copy (e.g. About → Events map, Home → Enquiry), not only through the nav; the footer repeats Enquiries and Contact on every page |
| Mobile-friendliness | Responsive layout (desktop / tablet ≤1024px / mobile ≤600px), viewport meta tag, tap-sized controls, hamburger nav, `skip-link` |
| Structured data (JSON-LD) | `Organization` (with `areaServed` = both cities, Home/About/Contact), `FAQPage` (Enquiry), `ContactPage` (Contact), `CollectionPage` (Events) |
| Social sharing | Open Graph + Twitter Card tags on every page so shared links show a title, description and photo |

| Page | Primary keyword focus |
|---|---|
| Home | Session 23, Amapiano events Gqeberha, House events Johannesburg |
| About | Party With The English, Amapiano collective, Port Elizabeth events |
| Events | upcoming Amapiano events, Hip-Hop events Johannesburg |
| Enquiry | book Amapiano event, brand partnership, campus event booking |
| Contact | contact Session 23, events Gqeberha / Johannesburg |

**3.2 Off-page SEO** (plan — these happen outside the codebase)

- **Backlinks:** link the website from the Instagram bio (`@Ses_sion23`) and every event post; ask the venues, DJs, photographers and partner brands from past nights to link to the site from their pages; list events on local what's-on and ticketing sites with a link back; ask campus societies and student media to link when Session 23 events are covered.
- **Social media:** each page carries Open Graph tags so shares look professional; Instagram is linked in the Contact details and in the footer of every page; post the Archive photos with a link to `events.html#archive`.
- **Local SEO:** both cities are named in titles, descriptions, headings, footer text and the JSON-LD `areaServed`; the map shows both cities; next step is claiming a Google Business Profile for Gqeberha and Johannesburg once there is a fixed venue/address.

**3.3 Additional requests**

- **`robots.txt`:** allows all pages, blocks `/documentation/` and `/images/screenshots/` (marker evidence, not search content) and points to the sitemap.
- **`sitemap.xml`:** the five pages with `lastmod`, `changefreq` and `priority` (Home 1.0, Events 0.9, Enquiry 0.8, About/Contact 0.7).
- **Page speed:** fonts loaded with `<link rel="preconnect">` + `display=swap` instead of a render-blocking CSS `@import`; every script is `defer`red; jQuery and Leaflet are only loaded on the pages that use them (Home and About load no libraries); lazy-loaded responsive images; the lightbox only fetches the large photo when opened; map tiles only load when the map is shown.
- **Security:** see the table below.

| Measure | Detail |
|---|---|
| Content-Security-Policy | Meta tag on every page restricting scripts to the site itself, forms/AJAX to the FormSubmit address and `mailto:`, images to the site and OpenStreetMap tiles, plus `object-src 'none'` and `base-uri 'self'` |
| Self-hosted libraries | jQuery and Leaflet live in `js/vendor/` and `css/vendor/`, so the site does not trust a third-party CDN with its scripts |
| XSS protection | All dynamic content is written with `textContent`/`createTextNode`; visitor input (search box, form fields) is never inserted as HTML. Tested with an `<img onerror>` payload in the search box |
| Input validation | Every form field validated on the client (and the receiving service validates again). HTML5 attributes (`required`, `type`, `maxlength`, `min`/`max`) are used in addition to JavaScript |
| Spam protection | Hidden honeypot field on both forms (bots fill it in, submissions are silently dropped) |
| Safe external links | `rel="noopener"` on every `target="_blank"` link; `referrer` meta policy `strict-origin-when-cross-origin` |
| HTTPS | Enforced by GitHub Pages / Netlify on the deployed site |
| Privacy | Consent tick box on both forms; Geolocation only on button press |

### 4. Form functionality and validation

**`enquiry.html` (services / bookings / partnerships)**

- Fields: name, email, phone, enquiry type (`<select>`), city (`<select>`), optional event, event date (`<input type="date">`), expected guests (`<input type="number">`), message (`<textarea>`), consent (`<input type="checkbox">`).
- **Validation:** required fields; name 2–60 letters; email format; South African phone numbers (`082 123 4567`, `+27 82 123 4567`, `0027…`); date must be today or later and within two years; guests a whole number from 10 to 5000; message 10–1000 characters with a live counter; consent ticked. Date and guests are only required for services that can be quoted.
- **Error handling:** inline `role="alert"` messages under each field, red border and `aria-invalid`, a summary message, focus moved to the first invalid field, errors clear as soon as the field is fixed.
- **Processing & response:** once valid, the form shows a response card with a reference number, an **indicative cost range** (base fee + per-guest rate from `js/data.js`, +/- range, travel allowance outside Gqeberha/Johannesburg, large-event note above 500 guests) and an **availability check** that compares the chosen date with the minimum lead time for that service (4 weeks private/campus, 6 weeks brand partnership, taken from the FAQ).
- **AJAX submission:** the form's `action` points at `https://formsubmit.co/contactsession23@gmail.com`; JavaScript intercepts the submit and sends it with `fetch()` as JSON, with a 12-second timeout, a busy state on the button, and a success or failure message. If delivery fails, a pre-filled `mailto:` link is shown so the enquiry is never lost. Without JavaScript the browser posts the form to the same `action`.

**`contact.html` (general messages)**

- Fields: name, email, optional phone, type of message (general / ticket support / media / feedback / other), subject, message, consent — same layout, validation and error handling as the enquiry form.
- **Email compilation:** once valid, the details are compiled into an email addressed to `contactsession23@gmail.com` (recipient set in `js/data.js` and the form `action`), shown in a review panel with **Open In My Email App** (a `mailto:` link with subject and body pre-filled), **Copy Email Text** and **Edit Message** buttons. The visitor sends the email themselves.
- **Form action:** `action="mailto:contactsession23@gmail.com"` is the no-JavaScript fallback.

### 5. Testing

The behaviour was tested with an automated jsdom script (events search/filter/sort/reset, modal, tabs and deep links, lightbox, map markers, every validation rule, enquiry cost and availability maths, AJAX success, failure and honeypot paths, contact email compilation, accordion). Also test by hand in a real browser: keyboard-only use of tabs/accordion/lightbox, a phone-width viewport, and Lighthouse (Performance / Accessibility / SEO) on the deployed URL.

## Deployment

The site is plain HTML/CSS/JS, so any free static host works.

**GitHub Pages** — push the repository, then **Settings → Pages → Source: `main` branch, `/ (root)` → Save**. The site appears at `https://<username>.github.io/session23-poe/`.
**Netlify (alternative)** — drag the project folder onto https://app.netlify.com/drop (no build settings needed).

After the URL is known, replace the placeholder everywhere (canonical links, Open Graph tags, JSON-LD, `sitemap.xml`, `robots.txt`):

```bash
grep -rl "YOUR-USERNAME.github.io/session23-poe" . --exclude-dir=.git | xargs sed -i 's#YOUR-USERNAME.github.io/session23-poe#<username>.github.io/<repo-name>#g'
```

The enquiry form uses FormSubmit: the **first** test submission sends an activation email to `contactsession23@gmail.com` — click the link in it once, and later enquiries arrive in that inbox.

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

### 2026-10-29 — Part 3: Enhancing Functionality and SEO

**Working through feedback from Part 2**

- **Render-blocking font import:** removed the CSS `@import` for Google Fonts and replaced it with `<link rel="preconnect">` + `<link rel="stylesheet">` in every page `<head>`, so the font request no longer waits for `style.css` to download.
- **Inline styles removed:** every `style="…"` attribute left over from Parts 1–2 (buttons, section borders, muted copy, testimonial footers, contact links) moved into reusable classes in `style.css` (`.link-gold`, `.btn-sm`, `.section-border`, `.copy-muted`, `.quote-by`, …), so layout can be changed from one file and overridden in media queries.
- **Invalid `<time datetime="">`:** removed the empty `datetime` attribute from events with unconfirmed dates (an empty value is invalid HTML); real `<time datetime="YYYY-MM-DD">` markup can be added when dates are confirmed. The events data now carries `date: null` until then.
- **Navigation consistency:** all five pages now use the same nav with `aria-label="Main"`, `aria-controls` on the menu button, and a "Skip to main content" link; the footer now links Enquiries as well as Contact on every page.
- **Gallery images:** the 1600px photos were re-encoded as progressive JPEG (quality 80), reducing the archive from about 2.09 MB to 1.87 MB with no visible loss.
- **TODO comments:** the in-page `TODO` comments were moved out of the HTML into the **Still To Do** list below, so no unfinished-work notes ship in the markup.
- **Internal linking and content:** added contextual links between pages (About → Events map, Home → Enquiry, Contact → Enquiry), and added Gqeberha/"Port Elizabeth" local wording to About and Contact.
- **Accessibility:** consistent `:focus-visible` outlines on all controls, labelled form fields with `aria-describedby`/`aria-invalid`, `role="alert"` errors and `aria-live` status messages.
- **Responsive evidence:** layout rules for the new components (filter bar, tabs, modals, forms, map) were added to the existing tablet and mobile breakpoints.
- **Contact page form (new):** the Contact page previously had only details. It now has a message form with the same fields, layout and validation as the Enquiry form (see section 4).

**New in Part 3**

- **`js/data.js` (new):** events, services, pricing rules and the contact email in one place.
- **`js/script.js`:** added the safe `el()` DOM helper, Escape-to-close on the mobile menu and the scroll-reveal animation (`IntersectionObserver`).
- **`js/interactive.js` (new, jQuery):** FAQ accordion, three-tab Events layout with deep links, native `<dialog>` modal and the gallery lightbox.
- **`js/events.js` (new):** events rendered dynamically with search (with match highlighting), city/genre filters and four sort orders.
- **`js/services.js` (new):** services rendered dynamically; "Choose This" fills the form.
- **`js/map.js` (new):** Leaflet map with a marker and event popup per city and a "Find my nearest city" geolocation button, on the Events (Map tab) and Contact pages.
- **`js/forms.js` (new):** shared validation rules, inline errors, character counter, honeypot, enquiry cost/availability response with AJAX submission and mailto fallback, and the contact email compiler.
- **`events.html`:** rebuilt around tabs (Upcoming / Archive / Map); the three static ticket cards were replaced with the dynamic list (with a `<noscript>` fallback); gallery links now open the lightbox.
- **`enquiry.html`:** added the services list, phone/city/date/guests/consent fields, the response card and the jQuery FAQ accordion (replacing the `<details>` elements).
- **`contact.html`:** added the contact form, email preview panel and map.
- **SEO:** new unique titles and meta descriptions, keywords, canonical links, Open Graph/Twitter tags, JSON-LD structured data, `robots.txt`, `sitemap.xml`, favicon and a custom `404.html`.
- **Security:** Content-Security-Policy and referrer policy meta tags, self-hosted jQuery and Leaflet, textContent-only DOM writes, honeypot spam trap, consent checkbox.
- **Vendor libraries:** jQuery 3.7.1 (MIT) and Leaflet 1.9.4 (BSD-2-Clause) added under `js/vendor/` and `css/vendor/` with their licences.

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

- [ ] Replace placeholder event dates/venues in `js/data.js`, `index.html` and `events.html` with confirmed details (set `date: 'YYYY-MM-DD'` in `data.js` and the "Soonest first" sort starts working)
- [ ] Review the indicative prices in `js/data.js` (`base`, `perGuest`) — they are starting-point placeholders
- [ ] Replace `YOUR-USERNAME` in the canonical/Open Graph/sitemap/robots URLs once the live URL is known (see **Deployment**)
- [ ] Click the FormSubmit activation email once after the first live test submission
- [ ] Re-run the screenshot evidence above (the images still show the Part 2 layout) and add Part 3 screenshots of the lightbox, map and form validation
- [ ] Add the live site URL and the GitHub repository link at the top of this README and submit the repository link on the LMS
- [ ] Run Lighthouse on the live site and note the scores
- [ ] Continue committing after every change (see **Git Workflow**)

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
- Leaflet (no date) *Leaflet — an open-source JavaScript library for interactive maps*. Available at: https://leafletjs.com/ (Accessed: 29 October 2026).
- jQuery Foundation (no date) *jQuery API Documentation*. Available at: https://api.jquery.com/ (Accessed: 29 October 2026).
- OpenStreetMap contributors (no date) *OpenStreetMap*. Available at: https://www.openstreetmap.org/copyright (Accessed: 29 October 2026).
- FormSubmit (no date) *FormSubmit documentation (AJAX)*. Available at: https://formsubmit.co/ajax-documentation (Accessed: 29 October 2026).
- Google (no date) *Search Engine Optimization (SEO) Starter Guide*. Available at: https://developers.google.com/search/docs/fundamentals/seo-starter-guide (Accessed: 29 October 2026).
- Google (no date) *Introduction to robots.txt* and *Build and submit a sitemap*. Available at: https://developers.google.com/search/docs/crawling-indexing/robots/intro (Accessed: 29 October 2026).
- Google (no date) *Intro to structured data markup*. Available at: https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data (Accessed: 29 October 2026).
- Mozilla Developer Network (no date) *<dialog>: The Dialog element*. Available at: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/dialog (Accessed: 29 October 2026).
- Mozilla Developer Network (no date) *Intersection Observer API*. Available at: https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API (Accessed: 29 October 2026).
- Mozilla Developer Network (no date) *Content Security Policy (CSP)*. Available at: https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP (Accessed: 29 October 2026).
- Mozilla Developer Network (no date) *Client-side form validation*. Available at: https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Form_validation (Accessed: 29 October 2026).
- Mozilla Developer Network (no date) *Geolocation API*. Available at: https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API (Accessed: 29 October 2026).
- World Wide Web Consortium (W3C) (no date) *ARIA Authoring Practices Guide: Tabs and Accordion patterns*. Available at: https://www.w3.org/WAI/ARIA/apg/patterns/ (Accessed: 29 October 2026).
- Open Web Application Security Project (OWASP) (no date) *Cross Site Scripting Prevention Cheat Sheet*. Available at: https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html (Accessed: 29 October 2026).
- GitHub (no date) *Creating a GitHub Pages site*. Available at: https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site (Accessed: 29 October 2026).
- Event photography: own photography, Session 23 events, Gqeberha (2026),
  reproduced with permission for use in this coursework project only.
