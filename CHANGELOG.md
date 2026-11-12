# Changelog

All notable changes to RomGoGetter Community Edition are documented here.

This is an unofficial community fork of [RomGoGetter](https://github.com/shokoe/RomGoGetter), originally developed by Shoko.

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
