# Ngeu'la' Mbäfeung — mobile calendar app

## What this is
Just the calendar, extracted from the original results-page mockup and rebuilt as its
own full-screen, mobile-only app. Everything unrelated (search results column, site
header/navbar, footer links, account icon, the small collapsed "widget" preview) has
been removed. The 8-day cycle logic, Mbäfeung month/weekday names, week numbering,
and the PDF export are carried over unchanged from the source file.

## Files
- `index.html` — markup + all styles (mobile-only, full-screen, no desktop layout)
- `calendar.js` — the data engine (weekday/month/cycle name tables, cycle math, week
  numbering) plus the rebuilt navigation (swipe, drawer, search, PDF export)
- `manifest.json` — installable-app manifest
- `icons/icon-144.png`, `icon-192.png`, `icon-512.png` — the app icons you supplied

## Navigation, as implemented
- **Day view** is the entry point.
- **Swipe left / right**: steps to the next/previous unit at the current level (day
  ±1 day, week ±8 days, month ±1 month, year ±1 year). Same slide animation as the
  source file (`calSlideNext` / `calSlidePrev`).
- **Swipe up**: zooms out one level (day→week→month→year), using the source's
  `calZoomOut` animation. Does nothing on the year view.
- **Swipe down**: zooms in one level (year→month→week→day), using `calZoomIn`. Does
  nothing on the day view.
- Left/right edge chevrons duplicate the swipe-left/right action for pointer users.
- **Hamburger (top-left)** slides a left-hand drawer over the current view listing
  Day / Week / Month / Year; the current view's label is dimmed. Tapping a label
  jumps straight there (zoom-in or zoom-out picked automatically depending on
  direction). Tapping anywhere outside the drawer closes it, on any page.
- **Search icon** opens the same day/month/year input popup as the source, with the
  same live validation (red border on out-of-range values, auto-advance between
  fields, Enter to go). Submitting always lands on the Day view for that date.
- **The boxed date badge (top right)** shows the real "today" day number and acts as
  the reload button: tap it to snap the current view back to today without changing
  which level (day/week/month/year) you're on.
- **Download** (circular button, bottom-right) appears only on Month and Year views
  and generates the exact same landscape A4 PDF layout as the source file (one page
  per month for Year, a single page for Month).
- **Share** screenshots whichever view is currently on screen and hands it to the Web
  Share API (falls back to a PNG download on desktop browsers without Share support).

## App icon
The app icon is a static logo (dark gradient background, "Mbäfeung" in white) used
everywhere — browser tab favicon, `apple-touch-icon`, and the manifest's home-screen
icons (`icon-144.png`, `icon-192.png`, `icon-512.png`). An earlier build experimented
with redrawing the tab favicon daily to show the current day number + cycle
abbreviation; that behavior has been removed so the icon stays consistent across
every surface. The manifest icons are also marked `"purpose": "any maskable"` since
the logo has enough padding around it to survive Android's adaptive-icon mask.

## Continuing this work — prompt for the next AI session
If you are picking this up: the app is functionally complete for the scope described
above (day/week/month/year navigation, swipe + drawer + search + PDF export + share,
mobile-only, full-screen, static logo icon set). Everything in this folder — the
calendar's data logic, its four views, and the navigation model (swipe up/down for
zoom, swipe left/right for step, hamburger drawer for direct jumps) — should be
treated as the working, finished baseline: extend it, don't re-derive it.
