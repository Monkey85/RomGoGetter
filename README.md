# RomGoGetter Community Edition v0.18.2

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

### Latest release — v0.18.2

This release focuses on download stability, arcade FixDAT matching and user interface consistency.

**Highlights:**
- Improved aria2c torrent downloads with Pause, Resume and Stop.
- Automatic cleanup of temporary directories after stopping downloads.
- Previously completed downloads are detected and skipped.
- Enhanced arcade clone-to-parent matching without requiring an additional reference DAT.
- Improved Download tab layout.
- Dark-themed Group Generator with native-style checkboxes.

## Directory Structure
RomGoGetter Community Edition stores its configuration files and the optional aria2c executable in a dedicated `data/` directory.

```text
RomGoGetter/
├── RomGoGetter_CE_v0.18.2.pyw
├── data/
│   ├── RomGoGetter_settings.json
│   ├── RomGoGetter_groups.json
│   ├── RomGoGetter_dat_groups.json
│   └── aria2c.exe
├── README.md
├── CHANGELOG.md
└── LICENSE
```

### Configuration Files
- `RomGoGetter_settings.json` — Application preferences and download settings.
- `RomGoGetter_groups.json` — Saved ROM source groups.
- `RomGoGetter_dat_groups.json` — Saved DAT groups.
- `aria2c.exe` — Optional download executable used for Minerva torrent downloads.

### Automatic Migration

When upgrading from an older Community Edition version, RomGoGetter automatically creates the `data/` directory and moves existing configuration files and `aria2c.exe` from the application root into it.

Existing files in `data/` are never overwritten by the migration process.

**Important:** Back up your configuration files before upgrading.

If `data/aria2c.exe` is not available, RomGoGetter can also use aria2c installed in the system PATH.

### aria2 Integration

RomGoGetter Community Edition includes `aria2c.exe` for Windows x64 in the `data/` directory.

The bundled executable is used for torrent-based downloads from supported sources, including Minerva.

No separate aria2 installation is required when using the bundled Windows x64 executable.

If the bundled executable is unavailable, RomGoGetter will attempt to locate aria2 through the system PATH.

**Third-party software notice:** aria2 is an independent open-source project distributed under the GNU General Public License v2.0 or later.

Official project: https://github.com/aria2/aria2

Licensing information and corresponding source code availability details are documented separately.

See [CHANGELOG.md](CHANGELOG.md) for the full list of changes.

**Download:** [RomGoGetter Community Edition releases](https://github.com/Monkey85/RomGoGetter/releases)

**Original project:** [RomGoGetter by Shoko](https://github.com/shokoe/RomGoGetter).

### Credits and attribution

**Original author:** [Shoko](https://github.com/shokoe)

**Community Edition maintainer:** [Monkey85](https://github.com/Monkey85)

This is an independent, unofficial fork and is not presented as an official release by the original author.

The original project is distributed under the MIT License. Copyright and license notices are retained.

### Development status

Community Edition v0.18.1 is an initial community build. Some functionality, particularly external download backends, requires additional testing.

---

# RomGoGetter v0.18

**ROM curator and downloader for archive.org, lolroms.com, Minerva, and local collections. It helps you to download only the roms you want from larger romsets.**

RomGoGetter started as a 1G1R tool — pick the best regional variant of each game and skip the rest. It has since grown into a full ROM curation pipeline: pull no-intro and redump listings from multiple repositories, apply smart filtering to build exactly the collection you want, then download or copy only what's needed.

---

## Requirements

- Python 3.10+
- tkinter (included with most Python distributions)
- `aria2c` — required for Minerva/Myrient downloads
- `cloudscraper` — required for Eden/EmuReady compatibility (`pip install cloudscraper`)
- `rapidfuzz` — optional but strongly recommended for Top N matching speed (`pip install rapidfuzz`)

---

### Installation

```
git clone https://github.com/shokoe/RomGoGetter
cd RomGoGetter
python RomGoGetter_v0_17.pyw
```
---

## Usage Examples

### Basic 1G1R download from archive.org

1. Setup tab
  a. Paste or select an archive.org collection URL(s) into **Source URLs / Local Dirs**
  b. Set a **Destination** folder
  c. Click on GoGet!
2. Selection tab
  a. Choose a **Mode**: `1G1R English only`
  b. Review selection and add or remove specific roms
  c. Click on **Cmopatibility** to filter by emulator compatibility lists or go straight to **Download**
3. Compatibility tab
  a. Choose the correct emaulator and click on **Fetch**
  b. Deselect groups by cards or use **Deselect below**
  c. Click on Download
4. Download tab
  a. Modify downdload settings
  b. Click on **Start**
5. Make coffeee and gaze at the dowloads ;)

### Top N by size budget

1. Set source URL(s) and destination
2. Set Mode to `Top N`
3. In the Selection tab, select source, platform, and **Max size GB**
4. Click **Fetch & Apply** — pages are fetched one at a time, full 1G1R selection is run after each page, and fetching stops as soon as the budget is reached
5. Click **Download**

### Smart copy from local collection

1. Paste your existing ROM directory path into **Source URLs / Local Dirs** (enable **Recursive** if files are in subdirectories)
2. Set **Destination** to a new folder
3. Click **GoGet!** — local files appear in the list with exact sizes
4. Apply Top N or 1G1R filtering, then click **Download** to copy selected files

### Eden (Switch) compatibility

1. Go to the **Compatibility** tab
2. Select **Eden (Switch)** as emulator
3. Click **Fetch Compatibility** — fetches from EmuReady, paginated, best score per title across all device reports
4. Requires `cloudscraper` (`pip install cloudscraper`)

### Minerva/Myrient

1. Paste a Minerva browse URL
2. This uses the bundled `aria2c.exe`
3. A torrent warning banner is shown as a reminder to seed via a proper torrent client

---

## Sources

- **archive.org** — fetches the file listing from any public (or credentialed) Internet Archive collection; supports S3 keys for access-restricted collections; works with "show all" and zip content pages
- **lolroms.com** — scrapes file listings and direct download URLs from category pages, including Wayback Machine snapshots
- **Minerva / Myrient** — downloads individual files from collection torrents via a full `aria2c` wrapper
- **Local directory** — paste a local folder path directly into the Source URLs input (one per line); local files are preferred over remote when the same filename exists in both. Enables using RomGoGetter as a **smart copy tool**: curate a large local collection down to a filtered subset in a new folder. Enable **Recursive** to scan subdirectories
- **Multiple sources at once** — paste multiple URLs and/or local paths (one per line); listings are merged into a single pool before filtering

---

## Selection

### 1G1R
The core mode. For each game title, picks one ROM: English preferred, highest revision, most language tracks. Excludes demos, kiosk builds, betas, prototypes, and non-game discs automatically.

### Modes

| Mode | Description |
|------|-------------|
| `1G1R English only` | One ROM per game, English/Western regions only, prefers multiple languages |
| `1G1R` | One ROM per game, best available region |
| `All files` | Every game ROM file selected |
| `None` | All files shown, none pre-selected — toggle manually |
| `DAT` | Cross-reference against a No-Intro / Redump DAT local or remote file; matched files selected, unmatched shown as missing |
| `Top N` | Filter by a ranked game list — see below |

### Top N
Fetches a ranked list of games from various well-known external source and maps them to your ROM pool using fuzzy/token title matching, then applies 1G1R within each matched group.

**Filter options:**
- **Top N** — take the N highest-ranked games
- **Min score** — take all games above a score threshold
- **Max size GB** — limit selection by cumulative size

### DAT Group
Apply multiple DAT files simultaneously (local paths or URLs). Useful for cross-referencing against a curated list spanning several platforms or sets.

### Bulk selection shortcuts
| Button | Action |
|--------|--------|
| `+` | Select all visible rows (doesn't touch others) |
| `-` | Deselect all visible rows (doesn't touch others) |
| `🕸` | Select visible, deselect everything else |

### Manual override
Double-click any file in the Selection tab to toggle it in or out of the download queue. The selected size card updates live.

### Missing files
A title is shown as **Missing** (red `✗`) when it was matched to a ROM in the file listing but that ROM is not available — not present in the local source and not found remotely. Missing rows cannot be selected.

---

## Download

- **Parallel slots** — up to 20 simultaneous downloads, adjustable live while downloading
- **Resume** — partial `.part` and torrented files are resumed automatically on retry
- **Stuck detection** — configurable idle timeout cancels and retries hung connections
- **Verification before skipping:**

| Mode | Behaviour |
|------|-----------|
| `Overwrite` | Always re-download |
| `Name` | Skip if file exists |
| `Size` | Skip if file exists and size matches |
| `Hash` | Skip if MD5 matches archive.org metadata; falls back to size; slow |

- **Local copy** — files sourced from a local directory are copied instead of downloaded, skipped if destination size already matches
- **Minerva torrents** — uses `aria2c` to fetch individual files by torrent index without downloading the full archive; temp torrent files are cleaned up after
- **Export DAT** — export the current selection as a No-Intro compatible DAT file

---

## File layout

```
RomGoGetter_v0.17.pyw        # main script
aria2c.exe                   # required for Minerva downloads (Windows)
RomGoGetter_settings.json    # auto-created, persists all settings
RomGoGetter_groups.json      # auto-created, persists URL groups
RomGoGetter_dat_groups.json  # auto-created, persists DAT groups
```

---

## Credits

- **[Internet Archive](https://archive.org)** — the world's library. [Donate](https://archive.org/donate)
- **[Myrient](https://myrient.erista.me)** — the team behind the Minerva Archive. [Memorial](https://minerva-archive.org/memorial/)
- **[lolroms.com](https://lolroms.com)** — [Donate](https://www.paypal.com/donate/?hosted_button_id=EG4YN6QGHCB6C)
- **[RetroAchievements](https://retroachievements.org)** — achievements and top lists for retro games
- **[IGDB](https://www.igdb.com)** — game database by Twitch
- **[EmuReady](https://www.emuready.com)** — community emulator compatibility tracker

---

## v0.18 Updates
- Minor fixes

---

## v0.17 Updates
Added compatebility check step for leading emulators!

### Selection Tab
- **Search now supports glob and regex** — plain text = substring match, `*`/`?` wildcards = glob, any regex special character (`.`, `+`, `[`, etc.) = regex
- **`+` / `-` / `🕸` bulk selection buttons** — `+` selects all visible rows in the current search, `-` deselects them (without touching rows outside the search), `🕸` selects only visible rows and deselects everything else
- **`Source URLs / Local Dirs`** — the URL input now accepts local directory paths alongside archive.org URLs, one per line; mixed sources are merged into a single pool
- **Recursive checkbox** — when enabled, local directory scans walk subdirectories; otherwise only the root is scanned

### Top N Mode
- Optimized matching speed

---

## v0.16 Updates
- Added support for TeknoParrot latest rom selection. The english only option doesn't work (and will not) so use the regex field to filter out Japan releases with `^(?!.*\(Japan\))`. You can also filter only the newest by year (i.e since 2020 - `20[2][0-9]`)

## v0.15 Updates
- Parallel fetch in setup
- Faster metadata fetch from IA
- Fixed a major IA URL bug that caused 404 error on download
- Font size controls
- Major site added to 'Top N' with genre selection support

---

## License

MIT — see [LICENSE](LICENSE)

© 2026 Shoko

---

<img width="1564" height="1236" alt="image" src="https://github.com/user-attachments/assets/349816f4-44fb-4483-91d0-146cf59444c3" />
<BR>
<img width="1561" height="1235" alt="image" src="https://github.com/user-attachments/assets/09ae6163-f49c-4709-aa05-0f9d6dcfad2a" />
<BR>
<img width="1561" height="1234" alt="image" src="https://github.com/user-attachments/assets/015ef6bd-406a-4116-b82d-3d20cccd0bc5" />
<BR>
<img width="1559" height="1231" alt="image" src="https://github.com/user-attachments/assets/ac5c64fe-c1ab-4026-8aa8-a3902479e60f" />


