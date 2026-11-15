# RomGoGetter Community Edition v0.18.3

**An unofficial community fork of [RomGoGetter](https://github.com/shokoe/RomGoGetter), originally developed by Shoko.**

This edition builds upon the original v0.18 release, introducing improvements to ROM selection, DAT matching, download management, and the user interface.

### Community Edition improvements

- Enhanced LoLROMs file discovery and matching.
- Custom ROM filters for betas, prototypes, demos, homebrew, and other categories.
- Improved No-Intro and arcade FixDAT handling.
- Group Generator for organizing source URLs.
- Improved group selection and autocomplete.
- Soft Reset without restarting the application.
- Download progress improvements and a Stop button.
- Dedicated Settings tab and reorganized navigation.
- New region and language filters in Selection, including multilingual filename support.

### Latest release — v0.18.3

This release adds region and language filtering to the Selection tab, with the same Community Edition visual style.

**Highlights:**
- **All Regions / All Languages**: default, unfiltered selection (backward compatible).
- **Filter by region**: select releases by filename region tags.
- **Filter by language**: recognize explicit language tags, including multilingual releases; use conservative regional inference otherwise.
- Available regions and languages are detected from the fetched ROM filenames and refresh on a new fetch.
- Filtering is performed **before** 1G1R's best-release selection.
- Reversed region/language tag order is recognized; ambiguous standalone tags are not assumed to be languages.
- Existing DAT and Top N modes retain their own selection rules and are not filtered by the new controls.

### Installation and requirements

- Windows with Python 3.10+ and Tkinter.
- Optional packages: `cloudscraper` for some compatibility sources; `rapidfuzz` for faster ranked-list matching.
- `aria2c` for torrent downloads; RomGoGetter looks for `data/aria2c.exe` or `aria2c` on PATH.

Launch `RomGoGetter_CE_v0.18.3.pyw` and use Setup to choose sources and a destination.

## Directory Structure

```text
RomGoGetter - CE/
├── RomGoGetter_CE_v0.18.3.pyw
├── README.md
├── CHANGELOG.md
├── LICENSE
├── data/
│   ├── RomGoGetter_settings.json
│   ├── RomGoGetter_groups.json
│   ├── RomGoGetter_dat_groups.json
│   └── aria2c.exe             (bundled in the GitHub project)
└── third_party/
    └── aria2/                 (third-party licensing documentation)
```

### Configuration Files
- `RomGoGetter_settings.json` — Application preferences and download settings.
- `RomGoGetter_groups.json` — Saved ROM source groups.
- `RomGoGetter_dat_groups.json` — Saved DAT groups.
- `aria2c.exe` — Download utility used for Minerva torrent downloads (Windows x64).

### Automatic Migration

When upgrading from an older Community Edition version, RomGoGetter automatically creates the `data/` directory and moves existing configuration files and `aria2c.exe` from the application root into it. Existing files in `data/` are never overwritten by the migration process.

**Important:** Back up your configuration files before upgrading. **Do not overwrite your own populated JSON settings with the clean sample files from a release archive.**

If `data/aria2c.exe` is unavailable, RomGoGetter can use aria2c installed in the system PATH.

### aria2 Integration

The GitHub project includes a Windows x64 aria2 executable in `data/`. aria2 is an independent project under GPL-2.0-or-later, not the application's MIT license. Keep the third-party notices and provide corresponding source access when redistributing it.

Official project: https://github.com/aria2/aria2

See [CHANGELOG.md](CHANGELOG.md) for the full list of changes.

**Download:** [RomGoGetter Community Edition releases](https://github.com/Monkey85/RomGoGetter/releases)

**Original project:** [RomGoGetter by Shoko](https://github.com/shokoe/RomGoGetter).

### Credits and attribution

**Original author:** [Shoko](https://github.com/shokoe)

**Community Edition maintainer:** [Monkey85](https://github.com/Monkey85)

This is an independent, unofficial fork and is not presented as an official release by the original author. Original MIT notices are retained.

---

# RomGoGetter v0.18 — Original project overview

**ROM curator and downloader for archive.org, lolroms.com, Minerva, and local collections. It helps you download only the ROMs you want from larger ROM sets.**

RomGoGetter started as a 1G1R tool: pick the preferred regional variant of each game and skip the rest. It now supports No-Intro and Redump listings from multiple repositories, filtering, and selective download or copy.

## Usage Examples

### Basic 1G1R download from archive.org
1. **Setup:** add an archive.org collection URL (or another supported source) and destination; click **GoGet!**.
2. **Selection:** choose 1G1R (or another selection mode), optionally set the region/language filter, then review the file list.
3. **Compatibility:** optionally fetch emulator compatibility ratings.
4. **Download:** set download options and click **Start**.

### Top N by size budget
1. Set source URLs and destination.
2. Set Mode to `Top N`.
3. Select source, platform, and **Max size GB**.
4. Click **Fetch & Apply**, then **Download**.

### Smart copy from local collection
1. Paste a local directory path into Source URLs / Local Dirs.
2. Enable Recursive for subdirectories, if needed.
3. Set a new destination, click GoGet!, then select and download (copy) files.

### Eden (Switch) compatibility
1. Go to the Compatibility tab.
2. Select Eden (Switch) and fetch compatibility data from EmuReady.
3. Install cloudscraper if needed: `pip install cloudscraper`.

### Minerva / Myrient
1. Paste a supported Minerva browse URL.
2. The downloader uses aria2c for torrent-based transfers.
3. Seed via a suitable torrent client where appropriate.

## Sources

- **archive.org** — public or credentialed Internet Archive collection listings.
- **lolroms.com** — listings and direct download URLs from categories, including archived listings where supported.
- **Minerva / Myrient** — individual files from collection torrents via aria2c.
- **Local directory** — smart copy from local collections, optionally recursive.
- **Multiple sources** — combine source URLs and local directories into one selection pool.

## Selection

### 1G1R
Chooses one ROM per title, considering region, revision, languages and exclusion rules. Default English-only 1G1R favors English/Western releases; standard 1G1R accepts other regions.

### Modes

| Mode | Description |
|------|-------------|
| `1G1R English only` | One English/Western ROM per title, with multilingual preference. |
| `1G1R` | One ROM per title, from the current candidate pool. |
| `All files` | Select every eligible ROM. |
| `None` | Show all ROM files without pre-selecting. |
| `DAT` | Match No-Intro or Redump DAT lists. |
| `Top N` | Match ranked external game lists. |

### Region / language filter (new in v0.18.3)

The **ROM filename filter** controls work on filenames returned by sources, without requiring a DAT or DB Export at runtime.

- `All Regions / All Languages` — disabled; same selection behavior as before.
- `Filter by region` — selects ROMs with the requested region tag.
- `Filter by language` — selects ROMs with the requested language, prioritizing explicit `(En,Fr,It)`-style tags and inferring from a region only when an explicit language list is unavailable.

Examples: `(Italy)` matches Italian; `(Europe) (En,Fr,It)` matches Italian; `(Europe) (En,Fr)` does not match Italian. Language tags may appear before region tags.

Language inference is a **filename heuristic**, not a guaranteed list of in-game languages. The filters are not applied by DAT and Top N modes.

### Top N
Supports ranked Top N, minimum score, and size-budget based selection using external lists.

### DAT Group
Apply multiple local or remote DAT files to a single fetched source list. Arcade parent archive matching is supported where source metadata permits it.

### Bulk selection shortcuts
- `+` — select all visible rows.
- `-` — deselect all visible rows.
- `🕸` — select visible, deselect the others.

### Manual override
Double-click a ROM in Selection to toggle it in the download queue. The selected-size card updates live.

## Download

- Parallel download slots with configurable retries.
- Resume support for interrupted transfers where supported.
- Stuck-download detection and configurable verification: Overwrite, Name, Size, Hash.
- Local-file copying to destination.
- Minerva torrents via aria2c.
- DAT export of the selected list.

## Credits

- [Internet Archive](https://archive.org)
- [Myrient](https://myrient.erista.me)
- [lolroms.com](https://lolroms.com)
- [RetroAchievements](https://retroachievements.org)
- [IGDB](https://www.igdb.com)
- [EmuReady](https://www.emuready.com)

## License

MIT — see [LICENSE](LICENSE).

© 2026 Shoko

## v0.18 Updates
- Minor fixes

## v0.17 Updates
Added compatebility check step for leading emulators!

### Selection Tab
- **Search now supports glob and regex** — plain text = substring match, `*`/`?` wildcards = glob, any regex special character (`.`, `+`, `[`, etc.) = regex
- **`+` / `-` / `🕸` bulk selection buttons** — `+` selects all visible rows in the current search, `-` deselects them (without touching rows outside the search), `🕸` selects only visible rows and deselects everything else
- **`Source URLs / Local Dirs`** — the URL input now accepts local directory paths alongside archive.org URLs, one per line; mixed sources are merged into a single pool
- **Recursive checkbox** — when enabled, local directory scans walk subdirectories; otherwise only the root is scanned

### Top N Mode
- Optimized matching speed

## v0.16 Updates
- Added support for TeknoParrot latest rom selection. The english only option doesn't work (and will not) so use the regex field to filter out Japan releases with `^(?!.*\(Japan\))`. You can also filter only the newest by year (i.e since 2020 - `20[2][0-9]`)

## v0.15 Updates
- Parallel fetch in setup
- Faster metadata fetch from IA
- Fixed a major IA URL bug that caused 404 error on download
- Font size controls
- Major site added to 'Top N' with genre selection support

---

<img width="1564" height="1236" alt="image" src="https://github.com/user-attachments/assets/349816f4-44fb-4483-91d0-146cf59444c3" />

<img width="1561" height="1235" alt="image" src="https://github.com/user-attachments/assets/09ae6163-f49c-4709-aa05-0f9d6dcfad2a" />

<img width="1561" height="1234" alt="image" src="https://github.com/user-attachments/assets/015ef6bd-406a-4116-b82d-3d20cccd0bc5" />

<img width="1559" height="1231" alt="image" src="https://github.com/user-attachments/assets/ac5c64fe-c1ab-4026-8aa8-a3902479e60f" />
