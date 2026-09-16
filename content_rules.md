# Content Structure (內容結構)

This document describes the organizational structure of the **Barren Rock Artchive (無用石 Barren Rock)** repository, as derived from the existing entries. Use it as the reference when adding, renaming, or migrating content.

## 1. Repository-level files

| File | Purpose |
|---|---|
| `README.md` | Project intro / build status ("building in progress"). Public-facing landing text. |
| `ABOUT.md` | Bilingual mission statement — the "美學 Aesthetics" and "無用石 Barren Rock" sections explaining the archive's name and critical stance. Currently Traditional Chinese only. |
| `CONTENT.md` | Master index of **all archived entries** — a year-grouped tree, newest year and newest entry first, each entry linking to its GitHub path with a one-line info summary underneath (see §9). Acts as the table of contents for the whole archive. |
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

### 4.1 Legacy entries (older front-matter schema)

Applies to entries carrying the older, simpler front-matter/body shape that predates the `text_template.md` schema (§4.2) — the files are now named `text-tc.md`/`text-en.md` like everything else (§3), but their front matter and body still follow this older shape. This is **not a clean date cutoff**: only about 22 of 55 `text-tc.md` files actually carry the legacy YAML front matter (`title`/`date`/`original_url`), scattered across years rather than confined to "before 2026" — it correlates more with whether an entry was migrated out of an old monthly compilation than with its publish date (see §8).

Body structure:
1. `# Title` (H1, matches front-matter title)
2. Metadata block: `展覽 Exhibition`, `策展人 Curator` (if any), `藝術家 Artist(s)`, `日期 Date` — plain text pairs, artist names listed in ascending last-name order, one per line.
3. For dead/external links: a short archival note ("*This article was originally published on ..., but the link is currently returning a 404 ... metadata has been preserved here for archival integrity.*") in place of full body text.
4. For full-text entries: `## Subheading` sections, body paragraphs, inline `![image](./img/imgN.jpg)` followed by an italic/plain caption line, and a `參考 Reference` section with linked citations at the end where applicable.
5. Monthly notes compilations (`筆記合集`, now fully split — see §6) used to repeat a mini metadata block (`展覽/電影 Exhibition or Film`, `藝術家/導演 Artist/Director`, `地點 Venue`, `日期 Date`) followed by a `## **Bolded sub-title**` and a short review, once per exhibition/film covered that month. Each split-out entry keeps that same legacy-schema shape, now under `Exh`/`Film`/`ExhPeriod`/`Venue`/`Artists`/`Directors` (§4.2) instead.

### 4.2 New/current format (`text_template.md`)

Legacy top-of-file YAML front matter (`title`/`date`/`original_url`, §4.1) is kept as-is for provenance when present. Exhibition/film/performance/etc. metadata itself lives in a plain fenced code block in the body, right after the `# Title` — not real YAML front matter, by deliberate choice, so it stays easy to hand-edit/read; it just needs to be internally consistent enough to script against later. All fields are optional — include only what's known. **The venue field name depends on content type** (confirmed across the archive, not a typo):

```
# Exhibition — venue field is "Space"
Exh: "title"
ExhPeriod: "ExhStartDate - ExhEndDate"
Space: "Artspace"
Artists: 
- "Artist1"
- "Artist2"
Curators: 
- "Curator1"

# Film
Film: "Film"
FilmYear: "FilmYear"
Directors:
- "Director1"

# Performance / music show — venue field is "Venue"
Perf: "Perf"
Venue: "Venue"
PerfDay: "PerfDay"
Artists:
- "Artist1"

# Design piece
DesignItem: "DesignItem"
DesignYear: "DesignYear"
Designers:
- "Designer1"
```

- Exhibitions use `Space` (e.g. `Space: "大館賽馬會藝方 Tai Kwun JC Contemporary"`); performances use `Venue` (e.g. `Venue: "大館 F Hall, Tai Kwun"`) — the two block shapes are genuinely different, not a naming slip.
- `ExhPeriod`/`PerfDay` aren't normalized to one date format in practice: dash ranges (`"2021-04-23 - 2021-08-01"`), dot ranges (`"2023.11.29 - 2023.12.12"`), and single dot-dates for one-day shows (`"2022.05.21"`) all appear.
- `Perf`/`PerfDay`/`Venue` are real and in active use (e.g. `2023-02-03 - 和光同塵`, `2021-10-31 - After Enso`), but every field beyond the type marker (`Perf`/`Exh`/`Film`/...) and `Artists` is optional — some `Perf` entries have no `Venue`/`PerfDay` at all.
- `DesignItem`/`DesignYear`/`Designers` are used (once so far: `2022-12-31 - 2022 年度我最喜愛展覽主視覺設計`). `Album`/`AlbumYear` are defined in `text_template.md` but not yet used by any entry.
- If a piece covers 2+ exhibitions/films/performances, add one separate fenced block per item immediately after the first — never merge them into one block/list (e.g. `2021-09-29 - 水泥城市` and `2023-12-31 - 墨洗／安全島` each carry two `Exh` blocks, each with its own `Curators`/`Space`).

Body (per `text_template.md`):
1. `# Title`
2. One (or more) info block(s) as above.
3. `---` divider, then a caption (H6) for the banner image immediately above it, then the banner image itself (`./img/banner.jpg`) — caption comes *before* the image it describes, not after.
4. Body organized under `### Subtitle N` headings — layout is flexible per piece. Every captioned image follows the same caption-then-image order; a caption may carry a footnote marker (`[^a1]`) for an artwork citation. Quotes use blockquote `>` with footnote markers (`[^1]`) for in-text citations.
5. Optional `---` divider followed directly by the footnote *definitions* — plain numeric (`[^1]: ...`) for in-text citations and `a`-prefixed (`[^a1]: ...`) for artwork captions, sitting together under the same divider with no subheading between them (only when any were used; the `a`-prefix exists purely so artwork-caption IDs never collide with citation IDs — it is not a separate section).
6. `---` + `#### 參考目錄 Reference List` — compulsory whenever there's any reading reference or artwork citation. In practice this is always **one flat numbered list** (`1.`, `2.`, ...) restating every footnote defined above, citations and artworks interleaved — there is no separate "作品 Artworks" heading/section on disk, despite what an earlier draft of this doc claimed. Artwork citations follow Harvard style: `藝術家（年份）。《藝術品名稱》。〔媒介〕。藝術空間，城市。` (TC/SC) or `Artist, A. (Year) *Title*. [Medium]. Venue, City.` (EN); omit the `〔媒介〕`/`[Medium]` bracket entirely when the medium isn't known rather than guessing.
7. Trailing `_` divider + `(pub.date)` line in `yyyy-mm-dd` format, with an optional `*notes` line after for personal post-notes.

Only reformat existing captions/citations into this footnote structure where the artwork/reference data is already present in the text (title, artist, year) — never fabricate a caption or citation for an image that was never captioned in the original.

This is a superset of the older archived-entry schema — new entries should follow `text_template.md`, saved as `text-tc.md`/`text-en.md` inside `Artchive/YYYY/YYYY-MM-DD - <Title>/` (§2), not the older `index-*.md` pattern.

## 5. Language policy

- Primary language: Traditional Chinese, frequently written in Cantonese vernacular (口語) rather than formal written Chinese.
- English titles/terms are kept inline for foreign artist names, exhibition titles, and quoted English-language sources.
- Every entry is intended to ship as a bilingual pair (`-tc` / `-en`), but English translations lag behind — many `text-en.md` files currently just carry an English `title` with untranslated Chinese body text.
- A `text-sc.md` (Simplified Chinese) variant exists for at least one entry (`Artchive/2025/2025-06-05 - 三文鱼丶Salmon丶鲑（さけ）/`, alongside `text-tc.md` and `text-en.md`) — not just a hypothetical future option, but a real trilingual precedent worth following for entries where SC readership matters.

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

All monthly `筆記合集` compilations have now been split into individual dated entries (§8). The archive currently has **59 entry folders** under `Artchive/` across 2021–2026 (2021: 25, 2022: 10, 2023: 18, 2024: 2, 2025: 2, 2026: 5, on-disk directory counts) — 55 of those have real text content; 4 of the 2026 folders are empty or placeholder (no file, or a 0-byte `text-tc.md`) and aren't real entries yet (see §8). Note `CONTENT.md`'s index table currently lags well behind this — see §8. Rather than re-listing every folder here (see `CONTENT.md` for the intended authoritative list with paths, once resynced), this shows the shape with a few representative entries per year:

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

## 9. CONTENT.md tree format

`CONTENT.md` is a year-grouped tree, not a table (an earlier version of both this doc and `CONTENT.md` used a flat markdown table — retired in favor of this). Rules:

- Group by year, newest year first (`2026` at the top); within a year, newest entry first by its folder date prefix.
- Only real entries with actual text content are listed — empty/placeholder folders (see §8) are left out entirely, not shown as stubs.
- Each entry's folder name is a markdown link to its GitHub path (`https://github.com/barrenrockaesthetics/BarrenRockArtchive/tree/main/Artchive/<year>/<folder>`), percent-encoded so the link works despite spaces/CJK/punctuation in folder names.
- Directly under the link, one line of **raw values** (no field labels) from that entry's info block (§4.2), pipe-separated (`|`), in the order the fields appear in the source file — e.g. `Exh | ExhPeriod | Space | Artists | Curators` for an exhibition, `Film | FilmYear | Directors` for a film. Multiple values within one field (e.g. several artists) are comma-joined within that field's slot, not given their own pipe segment.
- Entries with no info block at all (plain essays, e.g. `2023-09-29 - dampheat`) get `N/A` instead.
- Keep it minimal — this is a scannable index, not a synopsis; don't add commentary beyond what the info block already says.

Example (from the real file):
```
├── 2021/
│   ├── [2021-07-21 - 墨城：當代城市塑造的⽔墨](https://github.com/barrenrockaesthetics/BarrenRockArtchive/tree/main/Artchive/2021/2021-07-21%20-%20...)
│   │       墨城 Ink City | 2021-04-23 - 2021-08-01 | 大館賽馬會藝方 Tai Kwun JC Contemporary
```

When adding a new entry, regenerate/append to `CONTENT.md` rather than hand-copying an old row's shape — field order and presence genuinely differ by content type (§4.2).

