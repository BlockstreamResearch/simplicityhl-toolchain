# Changelog

## Unreleased 

### Breaking Changes
* Removed the `components` and `binstall-version` inputs from GitHub Action interface.
* Removed `simfmt-version` output from GitHub Action interface.
* Removed support for installing `simfmt` independently.
* To migrate, replace `components: simplex@0.2.0` with `simplex: 0.2.0`.

### Added
* Added the `simplex` input to select the `Simplex` version, defaulting to the latest stable release when omitted or empty.
* Added `CHANGELOG.md`

### Changed
* Install the selected `Simplex` toolchain, including its bundled simfmt binary for `Simplex` `0.2.0` and later.

### Fixed
* Fixed unauthenticated GitHub API rate-limit failures by using `GITHUB_TOKEN` in `curl` when downloading and running `simplexup`. 

## 0.0.2 - 2026-09-02

* Add `cargo-binstall` version parameter as an input value by @ikripaka in https://github.com/BlockstreamResearch/simplicityhl-toolchain/pull/2
* Add `CONTRIBUTING.md` by @ikripaka in https://github.com/BlockstreamResearch/simplicityhl-toolchain/pull/3

## 0.0.1 - 2026-09-01

* Initial release. Not recommended for production use.
