# Session 23 — Website (WEDE5020 PoE)

Static HTML/CSS/JS website built for **Session 23** ("Party With The English"), an
Amapiano, House and Hip-Hop events collective operating in Gqeberha and Johannesburg.

## Student

- Name: Luphawu
- Institution: The IIE Rosebank College
- Module: WEDE5020

## Live Site

GitHub Pages URL: *add once Pages is enabled — see setup steps below*

## Folder Structure

```
session23-poe/
├── index.html          # Homepage — hero, upcoming events preview, offerings
├── about.html           # Brand story, mission, vision, values
├── events.html          # Full events calendar / archive
├── enquiry.html         # Booking & partnership enquiry form
├── contact.html         # Contact details
├── css/
│   └── style.css        # Shared stylesheet (black & gold identity)
├── js/
│   └── script.js         # Shared script (mobile nav toggle)
├── images/               # Site images (add real event/brand photography here)
└── README.md
```

## Design Notes

- **Palette:** near-black background, muted gold (`#c9a227`) and bright gold
  (`#e8c661`) accents, cream text — matches the existing Session 23 brand identity.
- **Type:** Anton (display/headings) paired with Manrope (body) — a poster-style
  display face suited to an events brand, kept legible at body size.
- **Signature element:** the ticket-stub card (perforated divider) used for event
  listings, tying the UI back to physical event tickets.

## Still To Do Before Submission

- [ ] Replace placeholder event dates/venues in `index.html` and `events.html` with
      confirmed details
- [ ] Add real photography to `/images` and reference it in the Gallery section
- [ ] Confirm final contact email in `contact.html`
- [ ] Wire the enquiry form up to a real submission handler (e.g. Formspree) if required
- [ ] Add wireframes / references to the PoE document as required by the brief

## Setup — GitHub Pages

1. Push this repository to GitHub (public).
2. Go to **Settings → Pages**.
3. Under **Source**, select the `main` branch and `/ (root)` folder, then **Save**.
4. GitHub will publish the site at `https://<username>.github.io/<repo-name>/`.
