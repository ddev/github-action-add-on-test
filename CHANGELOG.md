# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en)
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## Public API

The [public API](https://semver.org/spec/v2.0.0.html#spec-item-1) of this project is defined by the `action.yaml` file.

---

## [v2.0.0](https://github.com/ddev/github-action-add-on-test/releases/tag/v2.0.0) - 2024-03-15

[_Compare with previous release_](https://github.com/ddev/github-action-add-on-test/compare/v1.2.0...v2.0.0)

### Changed

- **Breaking change**: Use `gautamkrishnar/keepalive-workflow@v2` to avoid dummy commit. This change requires 
  modifying permission from `contents: write` to `actions: write` in the main workflow.

---

## [v1.2.0](https://github.com/ddev/github-action-add-on-test/releases/tag/v1.2.0) - 2024-02-19

[_Compare with previous release_](https://github.com/ddev/github-action-add-on-test/compare/v1.1.1...v1.2.0)

### Changed

- Update `actions/checkout` to `v4` for Node.js 20 ([PR #26](https://github.com/ddev/github-action-add-on-test/pull/26))

---

## [v1.1.1](https://github.com/ddev/github-action-add-on-test/releases/tag/v1.1.1) - 2023-10-29

[_Compare with previous release_](https://github.com/ddev/github-action-add-on-test/compare/v1.1.0...v1.1.1)

### Fixed

- Turn off instrumentation for tests ([PR #23](https://github.com/ddev/github-action-add-on-test/pull/23))

---

## [v1.1.0](https://github.com/ddev/github-action-add-on-test/releases/tag/v1.1.0) - 2023-09-20

[_Compare with previous release_](https://github.com/ddev/github-action-add-on-test/compare/v1.0.0...v1.1.0)

### Changed

- Install `bats-file` by default ([@see PR #19](https://github.com/ddev/github-action-add-on-test/pull/19))

---

## [v1.0.0](https://github.com/ddev/github-action-add-on-test/releases/tag/v1.0.0) - 2023-08-25

[_Compare with previous release_](https://github.com/ddev/github-action-add-on-test/compare/v0.6.0...v1.0.0)

### Changed

- Install `bats-assert` and friends by default ([@see PR #15](https://github.com/ddev/github-action-add-on-test/pull/15))

---

## [v0.6.0](https://github.com/ddev/github-action-add-on-test/releases/tag/v0.6.0) - 2023-08-21

[_Compare with previous release_](https://github.com/ddev/github-action-add-on-test/compare/v0.5.0...v0.6.0)

### Changed

- Move (or create) the major version tag (such as `v1`, `v2`) to point to the Git ref of the current release ([@see #11](https://github.com/ddev/github-action-add-on-test/issues/11))

---

## [v0.5.0](https://github.com/ddev/github-action-add-on-test/releases/tag/v0.5.0) - 2023-08-21

[_Compare with previous release_](https://github.com/ddev/github-action-add-on-test/compare/v0.4.0...v0.5.0)

### Added

- Add `disable_checkout_action` boolean input ([@see #9](https://github.com/ddev/github-action-add-on-test/issues/9))

---

## [v0.4.0](https://github.com/ddev/github-action-add-on-test/releases/tag/v0.4.0) - 2023-08-21

[_Compare with previous release_](https://github.com/ddev/github-action-add-on-test/compare/v0.3.0...v0.4.0)

### Changed

- Run `keepalive-workflow` step even if a previous step failed

---

## [v0.3.0](https://github.com/ddev/github-action-add-on-test/releases/tag/v0.3.0) - 2023-08-11

[_Compare with previous release_](https://github.com/ddev/github-action-add-on-test/compare/v0.2.0...v0.3.0)

### Added

- Add `actions/checkout` and `gautamkrishnar/keepalive-workflow` steps in the action

---

## [v0.2.0](https://github.com/ddev/github-action-add-on-test/releases/tag/v0.2.0) - 2023-08-10

[_Compare with previous release_](https://github.com/ddev/github-action-add-on-test/compare/v0.1.0...v0.2.0)

### Removed

- Remove `edge` for `ddev_version` input

### Added

- Add `mxschmitt/action-tmate` and `Run test` steps in the action

---

## [v0.1.0](https://github.com/ddev/github-action-add-on-test/releases/tag/v0.1.0) - 2023-08-07

[_Compare with previous release_](https://github.com/ddev/github-action-add-on-test/compare/v0.0.1...v0.1.0)

### Changed

- Use choice (`stable`, `edge`, `HEAD`) for `ddev_version` input instead of a free string

---

## [v0.0.1](https://github.com/ddev/github-action-add-on-test/releases/tag/v0.0.1) - 2023-07-10

### Added

- Initial release
