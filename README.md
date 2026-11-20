# Sophia Hörhold – Portfolio

Hugo website for Sophia Hörhold, moderator and journalist. Layout "Sendeplan", color scheme "Tanne & Tomate".

All content lives in plain text files (Markdown, YAML, TOML). You never need to touch the theme in `themes/hoerhold/` to change texts, images, entries or categories.

## Quick start

Requires [Hugo](https://gohugo.io/installation/) (extended not needed), version 0.146 or newer.

```sh
hugo server          # preview at http://localhost:1313, reloads on every save
hugo                 # build the finished site into public/
```

Upload the contents of `public/` to any web host. To publish with GitHub and Netlify (automatic updates, no Terminal needed), follow **[PUBLISHING.md](PUBLISHING.md)**.

## Where is what?

The homepage, from top to bottom:

| Part of the page | File | Field |
|---|---|---|
| Name in the top left and the big name below it | `hugo.toml` | `name` (each word becomes its own line in the big name) |
| Menu (Arbeiten, Über mich, Kontakt) | `hugo.toml` | `[[menus.main]]` blocks |
| **Running ticker bar** below the name | `hugo.toml` | `roles` (list) and `city` |
| Portrait photo and photo credit | `content/_index.md` | `portrait`, `fotocredit` (image file in `static/img/`, see below) |
| Large intro sentence next to the portrait | `content/_index.md` | `intro` |
| Biography (two columns) | `content/_index.md` | the text below the closing `---` |
| Section headings ("Auswahl der Arbeiten", "Gearbeitet für", ...) | `content/_index.md` | `ueberschriften` |
| List of works ("Auswahl der Arbeiten") | `content/arbeiten/*.md` | one file per entry, see below |
| Upcoming dates ("Demnächst"), **hidden by default** | `data/termine.yaml` | see below |
| Clients ("Gearbeitet für") | `data/kunden.yaml` | one name per line |
| Quotes ("Stimmen") | `data/stimmen.yaml` | `text`, `wer`, `funktion` |
| Contact block: heading, e-mail, text, booking, social links | `hugo.toml` | `kontaktTitel`, `email`, `kontaktText`, `booking`, `instagram`, `linkedin` |
| Footer links | `content/impressum.md`, `content/datenschutz.md` | page text |
| Category pages (/moderation/ etc.) | `content/kategorien/<name>/_index.md` | see below |
| Color scheme | `hugo.toml` | `palette` |
| Browser tab icon (favicon) | `static/favicon.svg` | see below |

### Front matter in a nutshell

Markdown files start with a block between two `---` lines. That block is the *front matter*: settings in `key: value` form. Everything below the second `---` is the normal text of the page.

```markdown
---
title: Example
intro: A short sentence.
---

Normal text, *italic*, **bold**, [a link](https://example.org).
```

Put values that contain a colon `:` in quotes: `title: "Moderation: Podium"`.

## The running ticker bar

The ticker bar below the big name shows all roles followed by the city, repeated endlessly. Edit both in `hugo.toml`:

```toml
roles = ["Moderatorin", "Journalistin", "Host"]
city = "Leipzig & Berlin"
```

Add or remove roles as you like. The same roles are also used in the browser tab title and the page description for search engines. For visitors who have reduced motion turned on in their system settings, the ticker stays still.

## Changing the portrait and other images

All images live in `static/img/`. Everything in `static/` is published as is, so `static/img/portrait.jpg` becomes `/img/portrait.jpg` on the website.

To replace the portrait:

1. Copy the photo into `static/img/`, e.g. `static/img/portrait.jpg`. Portrait format 4:5 works best (e.g. 1600 × 2000 px); other formats are cropped to fit.
2. In `content/_index.md` change the line to `portrait: /img/portrait.jpg` and update `fotocredit`.

The photo gets a color tint matching the color scheme automatically. The placeholder files (`portrait.svg`, `still-1.svg` … `still-6.svg`) can be deleted once nothing refers to them anymore.

## The favicon

The small icon in the browser tab shows the initials "SH" in the colors of "Tanne & Tomate". It is the file `static/favicon.svg`, a short text file. To change the colors, open it and replace the two color codes (`#1d4433` background, `#f3eee4` letters). To use a different icon, replace the file with another SVG of the same name.

## Adding a new work entry

Each entry in "Auswahl der Arbeiten" is one file in `content/arbeiten/`. Copy an existing file, rename it (e.g. `09-tagesgespraech.md`) and adjust it:

```markdown
---
title: Das Tagesgespräch
sender: WDR 5
jahr: 2026
format: Live-Talk, 60 min
rolle: Moderation
bild: /img/tagesgespraech.jpg
kategorien: [Moderation]
link: https://www1.wdr.de/
weight: 9
---

Short description. Currently only used internally, not shown in the list.
```

| Field | Meaning |
|---|---|
| `title` | Title shown large in the list |
| `sender` | Broadcaster, client or venue |
| `jahr` | Year, shown in the first column |
| `format` | Format, e.g. "Podium" or "Feature, 54 min" |
| `rolle` | Her role, e.g. "Moderation" or "Autorin, Host" |
| `bild` | Still image that appears when hovering over the row (on phones it is always shown). Put the file into `static/img/` and write `/img/filename.jpg`. 16:9 works best. |
| `kategorien` | Exactly one category in square brackets: `[Moderation]`, `[Journalismus]` or `[Bildungsarbeit]` |
| `link` | *Optional.* If set, clicking the row opens this external page in a new tab (marked with ↗). If omitted, the row leads to the entry's category page (marked with →). |
| `weight` | Order in the list. Smaller numbers come first. |

Images get a color tint matching the color scheme automatically, so any photo works.

To remove an entry, delete its file.

## Adding new dates

The "Demnächst" section (upcoming events) is currently **switched off**. To use it:

1. In `hugo.toml` set `showTermine = true`.
2. Optionally add a menu entry in `hugo.toml`:
   ```toml
   [[menus.main]]
     name = "Termine"
     url = "/#termine"
     weight = 3
   ```
3. Add dates to `data/termine.yaml`:
   ```yaml
   - datum: 2027-06-12
     titel: Podiumsgespräch „Stadt für alle“
     ort: Schauspiel Leipzig
     rolle: Moderation
   ```

The date must be written as `YYYY-MM-DD`. Dates are sorted automatically. Past dates are **not** removed automatically, so delete them from the file once they are over.

## Adding a new category page

Categories group the work entries. Each category gets its own page (e.g. `/moderation/`) with a heading, an intro sentence, a text and the list of all entries in that category. The buttons at the top of each category page switch between categories.

Example: a new category "Podcast".

1. Create the folder and file `content/kategorien/podcast/_index.md`:
   ```markdown
   ---
   slug: podcast
   weight: 4
   title: Podcast
   intro: Eigene Podcasts und Gastauftritte.
   ---

   Longer text about this category (optional, shown in two columns).
   ```
   - `slug` is the address of the page (`/podcast/`). Use lowercase letters only, no umlauts or spaces: write `oe` for `ö`, `-` for spaces.
   - `weight` is the position in the category buttons.
   - `title` must be spelled exactly like the category in the work entries.
2. Assign entries to it in `content/arbeiten/*.md`:
   ```yaml
   kategorien: [Podcast]
   ```

A category page exists as soon as its `_index.md` exists, even with no entries yet. It then shows an empty list, so add entries before publishing.

If you skip step 1, the page is still created from the entries, but without intro text, and its address is taken from the category name as is, including umlauts (e.g. `/hörspiel/`). Always create the `_index.md` with a clean `slug`.

To delete a category, remove its folder in `content/kategorien/` and move its entries to another category.

To rename a category, change `title` in its `_index.md` **and** the `kategorien` field in all of its entries.

Existing categories:

| Category | File | Address |
|---|---|---|
| Moderation | `content/kategorien/moderation/_index.md` | `/moderation/` |
| Journalismus | `content/kategorien/journalismus/_index.md` | `/journalismus/` |
| Bildungsarbeit | `content/kategorien/bildungsarbeit/_index.md` | `/bildungsarbeit/` |

## Changing the color scheme

In `hugo.toml`:

```toml
palette = "tannetomate"
```

The current and earlier proposals are available: `tannetomate`, `navymandarine`, `beeresenf`, `petrolpink`, `ziegelhimmel`, `tanne`, `cognac`, `nacht`, `schoko`, `pinie`, `bordeaux`, `sand`.

To compare them in the browser, set `drafts = true` in `hugo.toml` and remove the `build:` block from `content/farben.md`. A bar at the bottom of every page then switches between schemes, and `/farben/` shows all of them side by side. Set `drafts = false` again before publishing.

The colors themselves are defined at the top of `themes/hoerhold/assets/css/main.css`.

## Before going live

- [ ] Replace all placeholder texts, images (`static/img/`) and the e-mail address
- [ ] Set the real domain as `baseURL` in `hugo.toml`
- [ ] Fill in `content/impressum.md` and `content/datenschutz.md` with legally valid texts
- [ ] Check that `drafts = false` is set

Fonts (Archivo, Newsreader) are hosted on the site itself. The site makes no requests to Google or other third parties and sets no cookies.

## Folder overview

```
hugo.toml                  site settings: name, ticker, contact, menu, colors
content/
  _index.md                homepage: intro, portrait, biography, section headings
  arbeiten/                one file per work entry
  kategorien/              one folder per category page
  impressum.md, datenschutz.md
  entwuerfe/, farben.md    design drafts, not published
data/
  kunden.yaml              clients
  stimmen.yaml             quotes
  termine.yaml             upcoming dates
  paletten.yaml            color schemes for the comparison page
static/
  favicon.svg              browser tab icon
  img/                     portrait and work images
themes/hoerhold/           layout, styles, fonts; no changes needed for content
```
