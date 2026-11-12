# Changelog

All notable changes to RomGoGetter Community Edition are documented here.

This is an unofficial community fork of [RomGoGetter](https://github.com/shokoe/RomGoGetter), originally developed by Shoko.

## [0.18.2] - 2026-11-12

### Added
- Native-style checkboxes in the Group Generator, aligned with the Custom ROM Filter interface.
- Improved diagnostic logging for aria2c Pause/Resume operations.

### Improved
- aria2c download management, including parallel downloads, Pause, Resume and Stop.
- Global download progress reporting.
- Download session reset and cleanup of temporary `thread_###` directories after cancellation.
- Detection and skipping of previously completed downloads.
- Error handling when copying downloaded files to their final destination.
- Download tab layout, removing unnecessary outer scrolling.
- Group Generator visual consistency, including dark table styling, font alignment and dedicated checkbox column.
- Arcade FixDAT matching, including clone-to-parent fallback using `cloneof` and controlled `romof` relationships.
- Handling of missing arcade archives without requiring a separate parent reference DAT.

### Changed

- Moved application configuration files into a dedicated `data/` directory.
- Updated configuration loading and saving paths for `RomGoGetter_settings.json`, `RomGoGetter_groups.json`, and `RomGoGetter_dat_groups.json`.
- Updated aria2c executable discovery to use `data/aria2c.exe`.
- Added automatic migration of existing configuration files from the application root directory to `data/`, without overwriting existing destination files.
- Preserved fallback support for aria2c installed in the system PATH.

### Removed
- The optional "Arcade parent reference DAT" field and its associated processing.
- Redundant external scrolling in the Download tab.

### Fixed
- Incorrect Missing results for arcade clones when a matching parent archive is available.
- Download progress and interface state remaining visible after Stop.
- Incomplete aria2c temporary directories remaining after a stopped download.
- Inconsistent checkbox appearance and alignment in the Group Generator.

### Testing
- Verified parallel downloads using Minerva torrent sources.
- Verified Pause, Resume and Stop during real downloads.
- Verified cleanup of temporary download directories.
- Verified detection and skipping of previously downloaded files.
- Verified arcade FixDAT parent fallback during real ROM set rebuilding.

### Known limitations
- Arcade parent fallback depends on the metadata available in the FixDAT; not all ROM sets have been tested.
- Error handling has not been tested against every possible filesystem or network failure.
- External compatibility database availability depends on third-party services.

### Credits
- Original project: [Shoko](https://github.com/shokoe/RomGoGetter)
- Community Edition: [Monkey85](https://github.com/Monkey85)

This is an unofficial community-maintained fork. Original copyright and license notices are retained.

## [0.18.1] - 2026-11-12

Initial Community Edition release, based on RomGoGetter v0.18.

### Added

- Custom ROM filtering with inclusion and exclusion modes.
- Additional filtering options for beta, prototype, demo, sample, homebrew and other ROM categories.
- Group Generator for creating and managing URL collections.
- Group selection suggestions and autocomplete.
- Dedicated Settings tab.
- Stop button for interrupting download sessions.
- Community Edition version identification.

### Improved

- LoLROMs filename discovery, including beta and sample releases.
- ROM matching when using FixDAT files.
- No-Intro and arcade DAT handling, including parent/clone relationships.
- Setup Group selection and destination path handling.
- Global download progress reporting when file sizes are initially unknown.
- Download interface reset after stopping a session.
- Navigation order: Setup, Selection, Download, Group Generator, Compatibility, Settings.

### Changed

- Reset now clears the current session without restarting the Python application.
- Custom filters reset to "Exclude selected" with no categories selected.
- Stopping an HTTP download session removes incomplete `.part` files while preserving completed files.

### Known limitations

- Download cancellation and recovery with external aria2c processes require further testing.
- Compatibility results depend on external databases and title matching.
- This release has been developed and primarily tested on Windows.

### Credits

- **Original project:** Shoko — [RomGoGetter](https://github.com/shokoe/RomGoGetter)
- **Community Edition:** [Monkey85](https://github.com/Monkey85)

The original copyright and license notices are retained.
