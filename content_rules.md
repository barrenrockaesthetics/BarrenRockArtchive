# Content Structure (內容結構)

This document describes the organizational structure of the **Barren Rock Artchive (無用石 Barren Rock)** repository, as derived from the existing entries. Use it as the reference when adding, renaming, or migrating content.

## 1. Repository-level files

| File | Purpose |
|---|---|
| `README.md` | Project intro / build status ("building in progress"). Public-facing landing text. |
| `ABOUT.md` | Bilingual mission statement — the "美學 Aesthetics" and "無用石 Barren Rock" sections explaining the archive's name and critical stance. Currently Traditional Chinese only. |
| `CONTENT.md` | Master index table of **all archived entries** — columns: `#`, Date Written, Exhibition Date, Exhibition/Writing Name, Artist(s), Full Path. Acts as the table of contents for the whole archive. |
| `content_rules.md` | This file — documents the structure/conventions so new entries stay consistent. |
| `text_template.md` | Canonical Markdown template for writing a **new** entry body (see §4). |
| `Artchive/` | Directory holding every dated entry, grouped by year (see §2, §7). |

## 2. Entry folder naming convention

Each critique/exhibition/journal entry lives inside `Artchive/<YYYY>/`, in its own folder:

```
Artchive/YYYY/YYYY-MM-DD - <Title>/
```

- **Date prefix**: full publish date, `YYYY-MM-DD` (day precision, not month-level).
- **Title**: original title only — no suffix. Exhibition type (solo/group), attribution to a guest critic, or artist name are recorded in the entry's front matter / metadata block, not in the folder name.
- Monthly notes round-ups (`筆記合集`) are discontinued as a bundled format going forward — see §6.

## 3. Files inside each entry folder

| File | Required? | Purpose |
|---|---|---|
| `text-tc.md` | Yes | Traditional Chinese (often Cantonese vernacular) version — the primary/original text. |
| `text-en.md` | Yes | English counterpart. For externally-sourced/archived posts this is often identical Chinese content with an English `title` in front matter (not yet translated) — a placeholder rather than a full translation. |
| `img/banner.jpg\|png`, `img/img1.jpg\|png`, `img/img2.jpg\|png`, ... | Optional | Images referenced from the body text, matching the `./img/banner.jpg`, `./img/img1.jpg` paths used in `text_template.md`. Only present when the piece embeds images; capped at 1920px on the long edge to keep the repo lightweight (see §8). |

`<folder name> - pub at YYYY-MM-DD.pdf` (archival PDF snapshot of the published piece) is no longer part of the convention — all 9 were removed for file size (see §8).

## 4. Front matter & body schema

### 4.1 Legacy entries (pre-2026 front-matter schema)

Applies to entries written before the `text_template.md` schema (§4.2) was adopted — the files are now named `text-tc.md`/`text-en.md` like everything else (§3), but their front matter and body still follow this older, simpler shape:

YAML front matter, minimal set:

```yaml
---
title: "..."
date: "YYYY.MM.DD"        # or "YYYY.MM" for monthly compilations
original_url: "https://..."
status: "external_inactive"  # present when the original source link is dead
---
```

Body structure:
1. `# Title` (H1, matches front-matter title)
2. Metadata block: `展覽 Exhibition`, `策展人 Curator` (if any), `藝術家 Artist(s)`, `日期 Date` — plain text pairs, artist names listed in ascending last-name order, one per line.
3. For dead/external links: a short archival note ("*This article was originally published on ..., but the link is currently returning a 404 ... metadata has been preserved here for archival integrity.*") in place of full body text.
4. For full-text entries: `## Subheading` sections, body paragraphs, inline `![image](./img/imgN.jpg)` followed by an italic/plain caption line, and a `參考 Reference` section with linked citations at the end where applicable.
5. Monthly notes compilations (`筆記合集`, now fully split — see §6) used to repeat a mini metadata block (`展覽/電影 Exhibition or Film`, `藝術家/導演 Artist/Director`, `地點 Venue`, `日期 Date`) followed by a `## **Bolded sub-title**` and a short review, once per exhibition/film covered that month. Each split-out entry keeps that same legacy-schema shape, now under `Exh`/`Film`/`ExhPeriod`/`Venue`/`Artists`/`Directors` (§4.2) instead.

### 4.2 New/current format (`text_template.md`)

Legacy top-of-file YAML front matter (`title`/`date`/`original_url`, §4.1) is kept as-is for provenance. Exhibition (or film) metadata itself now lives in a plain fenced code block in the body, right after the `# Title` — not real YAML front matter, by deliberate choice, so it stays easy to hand-edit/read; it just needs to be internally consistent enough to script against later. All fields are optional — include only what's known:

```
Exh: "title"
ExhPeriod: "ExhStartDate - ExhEndDate"
Venue: "Venue"
Artists: 
- "Artist1"
- "Artist2"
Curators: 
- "Curator1"
Designers:
- "Designer"
Film: "Film"
FilmYear: "FilmYear"
Directors:
- "Director1"
```

If the piece covers 2+ exhibitions or films, add one separate fenced block per exhibition/film immediately after the first — never merge them into one block/list.

Body (per `text_template.md`):
1. `# Title`
2. One (or more) info block(s) as above.
3. `---` divider, then a caption (H6) for the banner image immediately above it, then the banner image itself (`./img/banner.jpg`) — caption comes *before* the image it describes, not after.
4. Body organized under `### Subtitle N` headings — layout is flexible per piece. Every captioned image follows the same caption-then-image order; a caption may carry a footnote marker (`[^a1]`) linking it to an `Artworks` entry. Quotes use blockquote `>` with footnote markers (`[^1]`) for in-text citations.
5. Optional `---` + `### 參考 Reference` footnote-definition block (`[^1]: ...`) at the end, for citations/references — only if any were used.
6. `---` + `### 作品 Artworks` section whenever an image cites an artwork (optional for film/music critique): footnote-style definitions (`[^a1]: artwork1`, using an `a`-prefixed namespace so IDs never collide with `Reference`'s plain-numeric footnotes).
7. Trailing `(pub.date)` line in `yyyy-mm-dd` format.

Only reformat existing captions/citations into this footnote structure where the artwork/reference data is already present in the text (title, artist, year) — never fabricate a caption or citation for an image that was never captioned in the original.

This is a superset of the older archived-entry schema — new entries should follow `text_template.md`, saved as `text-tc.md`/`text-en.md` inside `Artchive/YYYY/YYYY-MM-DD - <Title>/` (§2), not the older `index-*.md` pattern.

## 5. Language policy

- Primary language: Traditional Chinese, frequently written in Cantonese vernacular (口語) rather than formal written Chinese.
- English titles/terms are kept inline for foreign artist names, exhibition titles, and quoted English-language sources.
- Every entry is intended to ship as a bilingual pair (`-tc` / `-en`), but English translations lag behind — many `text-en.md` files currently just carry an English `title` with untranslated Chinese body text.

## 6. Content categories

1. **Exhibition/artwork reviews** — a single critique of one exhibition or artwork, solo or group, one folder per piece. Whether it's a solo or group show, and any guest authorship or artist attribution, lives in the front matter/metadata block (§4) rather than the folder name.
2. **Guest/attributed pieces** — written by, or focused on, a named critic or artist other than the archive's own voice; distinguished by metadata, not a folder suffix.
3. **Monthly notes compilations (discontinued, fully split)** — `YYYY.MM 筆記合集` was a running journal bundling short-form reviews (exhibitions, films, occasionally music/performance) written across a given month into one file. This format is retired: every historical compilation has been split into its own singular, dated entry (`Artchive/YYYY/YYYY-MM-DD - <Title>/text-tc.md`/`text-en.md`), and no `筆記合集` folders remain in the archive.

## 7. Directory tree

### 7.1 Generic pattern (target structure going forward)

```
BarrenRockArtchive/
├── README.md
├── ABOUT.md
├── CONTENT.md
├── content_rules.md
├── text_template.md
└── Artchive/
    ├── YYYY/
    │   ├── YYYY-MM-DD - <Title>/
    │   │   ├── text-tc.md
    │   │   ├── text-en.md
    │   │   └── img/                                     # optional; capped at 1920px long edge
    │   │       ├── banner.jpg|png
    │   │       ├── img1.jpg|png
    │   │       ├── img2.jpg|png
    │   │       └── ...
    │   └── YYYY-MM-DD - <Title>/
    │       └── ...
    └── YYYY/
        └── ...
```

### 7.2 Actual repository tree (current on-disk state, abridged)

All monthly `筆記合集` compilations have now been split into individual dated entries (§8) — the archive is 36 entries across 2021–2026. Rather than re-listing every folder here (see `CONTENT.md` for the authoritative, complete list with paths), this shows the shape with a few representative entries per year:

```
.
├── ABOUT.md
├── CONTENT.md
├── content_rules.md
├── README.md
├── text_template.md
└── Artchive/
    ├── 2021/
    │   ├── 2021-07-21 - 墨城：當代城市塑造的⽔墨/
    │   │   └── text-tc.md
    │   ├── 2021-08-13 - Sam Gilliam/                # split out of the old 2021.08 筆記合集
    │   │   ├── text-en.md
    │   │   └── text-tc.md
    │   ├── 2021-08-20 - 演練未來？/
    │   │   ├── img/
    │   │   │   ├── banner.jpg, img1.jpg … img5.jpg  # capped at 1920px long edge
    │   │   ├── text-en.md
    │   │   └── text-tc.md
    │   └── ...
    ├── 2022/
    │   ├── 2022-01-04 - 遊樂場記，2021/
    │   │   ├── img/
    │   │   │   ├── banner.png, img1.png … img6.png
    │   │   ├── text-en.md
    │   │   └── text-tc.md
    │   ├── 2022-05-21 - 不能承受的輕/                 # split out of the old 2022.05 筆記合集
    │   │   └── text-tc.md                            # no English version was ever written for this one
    │   └── ...
    ├── 2023/
    │   ├── 2023-02-01 - seeing the inside of eyeballs/
    │   │   ├── img/
    │   │   │   ├── banner.jpg, img1.jpg … img9.jpg
    │   │   ├── text-en.md
    │   │   └── text-tc.md
    │   └── ...
    └── ... (2024, 2025, 2026)
```

> This tree is illustrative, not exhaustive or byte-for-byte current — the archive keeps growing (new years, new entries, occasional `text-sc.md` for Simplified Chinese) faster than this doc is refreshed. See `CONTENT.md` for the authoritative, up-to-date list of every entry and its path.

## 8. Open inconsistencies to resolve

Resolved by decision and migration (see §2, §3, §6, §7):
- ~~Suffix (`- 聯展` / person name) in folder names~~ — dropped; folders are publish date + title only.
- ~~Month-level folder dates~~ — dated-piece folders now use full `YYYY-MM-DD`.
- ~~Physical migration~~ — all 18 pre-existing entries and the standalone `index_tc.md` (moved to `Artchive/2026/2026-06-03 - 我的私生活很亂，歡迎光臨/text-tc.md`) have been moved into `Artchive/YYYY/...` with `index-*.md` → `text-*.md`, `images/image_N` → `img/imgN`, and PDF filenames updated to match their new folder names.
- ~~Info-block metadata format~~ — reformatted to the `Exh`/`ExhPeriod`/`Venue`/`Artists`/`Curators` fenced block (§4.2) across every non-compilation entry.
- ~~Monthly notes compilations as an ongoing bundled format~~ — discontinued, and retroactively split: all 9 compilation files (27 items total) were broken into individual dated entries with their own `Exh`/`Film`/`Artists`/`Directors` blocks. No `筆記合集` folders remain.
- ~~PDF exports and oversized images bloating the repo~~ — all 9 `pub at YYYY-MM-DD.pdf` archival snapshots removed (they embedded full-resolution photos and ran 16–64MB each, ~183MB total). Every standalone image in `img/` resized to a 1920px long-edge cap; originals backed up outside the repo before touching anything. `Artchive/` went from ~390MB to ~28MB.

Still open:
- **Two content types the current schema doesn't cover**: a music concert (`Artchive/2023/2023-02-03 - 和光同塵`) and a performance-art piece (`Artchive/2021/2021-10-31 - After Enso`) were folded into the `Exh` field for lack of a better one — there's no `Music`/`Performance` field in `text_template.md`. Worth a decision if these categories recur.
- **Non-exhibition essays have no home in the schema**: （給自己的）藝術評論倫理學 responds to a published article, not an exhibition, and has no `Exh`/`Film` data at all — it was left with its legacy plain-text metadata rather than force-fit into the new info block.
- A few split-out entries have no `text-en.md` because no English version ever existed for that specific item in the original compilation (`2022-05-21 - 不能承受的輕` is one); not fabricated, just absent.
- The migrated `Artchive/2026/2026-06-03 - 我的私生活很亂，歡迎光臨/` entry has no `text-en.md` yet — needs an English counterpart to satisfy §3.
- `ABOUT.md` has no English counterpart yet (`ABOUT-en.md` does not exist), despite the site being framed as bilingual.
