# DDEV add-on test action

---

> A GitHub action to run tests on a DDEV add-on.

---

[![Version](https://img.shields.io/github/v/release/ddev/github-action-add-on-test)](https://github.com/ddev/github-action-add-on-test/releases)
![project is maintained](https://img.shields.io/maintenance/yes/2024.svg)
[![tests](https://github.com/ddev/github-action-add-on-test/actions/workflows/add-ons-test.yml/badge.svg)](https://github.com/ddev/github-action-add-on-test/actions/workflows/add-ons-test.yml)

**Table of Contents**

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Quick start](#quick-start)
- [Inputs](#inputs)
  - [Available keys](#available-keys)
- [Usage](#usage)
  - [Test your DDEV add-on](#test-your-ddev-add-on)
- [License](#license)
- [Contribute](#contribute)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Quick start

_We will suppose here that you want to test your add-on with the stable version of DDEV._

You can add the following step in your workflow:

```yaml
- uses: ddev/github-action-add-on-test@v2
  with:
    ddev_version: "stable"
    token: ${{ secrets.GITHUB_TOKEN }}
    addon_repository: ${{ env.GITHUB_REPOSITORY }}
    addon_ref: ${{ env.GITHUB_REF }}
```

This step will install the latest stable version of DDEV and run `bats tests` command from the source folder of your add-on.

(The source folder of your add-on must contain a `tests` folder with at least a `bats` file, as it is the case if you have used the [DDEV addon template](https://github.com/ddev/ddev-addon-template) to create your add-on.)

## Inputs

### Available keys

The following keys are available as `step.with` keys:

---

- `ddev_version` (_String_)

DDEV version that will be installed before your tests.

Not required.

Default: `stable`.

Allowed values are: `stable`, `HEAD`.

---

- `token` (_String_)

A GitHub Personal Access Token used by the `debug` and `run test` steps.

Required.

Example: `${{ secrets.GITHUB_TOKEN }}`.

---

- `addon_repository`(_String_)

GitHub repository of the tested addon (`{owner}/{repo}`). Will be used as the `repository` key during a [checkout
action](https://github.com/actions/checkout#usage)

Required.

Example: `${{ env.GITHUB_REPOSITORY }}`.

---

- `addon_ref`(_String_)

GitHub reference of the tested addon. Will be used as the `ref` key during a [checkout action](https://github.com/actions/checkout#usage)

Required.

Example: `${{ env.GITHUB_REF }}`.

---

- `addon_path`(_String_)

Path (relative to `$GITHUB_WORKSPACE` ) where the addon will be cloned by a checkout action. Will be used as the `path`
key of the [checkout action](https://github.com/actions/checkout#usage)

Not required.

Default: `./`

---

- `keepalive` (_Boolean_)

Keeps GitHub from turning off tests after 60 days.

If enabled, action will use [keepalive-workflow action](https://github.com/gautamkrishnar/keepalive-workflow) when `ddev_version` has been set to `stable`.

**N.B.** If enabled, you have to update the permission of the main workflow to `write`:

```yaml
permissions:
  actions: write
```

Not required.

Default: `true`.

---

- `keepalive_time_elapsed` (_String_)

Time elapsed from the previous commit to keep the repository active using GitHub API (in days).

Will be used as the `time_elapsed` key of the [keepalive-workflow action](https://github.com/gautamkrishnar/keepalive-workflow).

Not required.

Default: `"0"`.

---

- `debug_enabled` (_Boolean_)

If `true`, a tmate session will be accessible before the tests step. See [action-tmate](https://github.com/mxschmitt/action-tmate) for more details.

Not required.

Default: `false`.

---

- `disable_checkout_action` (_Boolean_)

If you need to check out your add-on source code with some specific inputs (`submodules`, `ssh-key`, etc.), or you need to perform some extra steps between checkout and DDEV installation steps, you can disable the default checkout action by setting `true` for this input.

Not required.

Default: `false`.

---

- `test_command` (_String_)

If you want to run a customized test command, you can use this input.

If it's empty, the test command will be `bats tests --filter-tags !release` during a pull request workflow and `bats tests` otherwise.

Not required.

Default: `""`.

---

## Usage

### Test your DDEV add-on

If your add-on is based on the [DDEV add-on template repository](https://github.com/ddev/ddev-addon-template), you
should have a tests folder containing a `test.bats` file.

Using this GitHub action, a `.github/workflows/tests.yml` file could have the following content:

```yaml
name: tests
on:
  pull_request:
  push:
    branches: [main]
    paths-ignore:
      - "**.md"

  schedule:
    - cron: "25 08 * * *"

  workflow_dispatch:
    inputs:
      debug_enabled:
        type: boolean
        description: Debug with tmate
        default: false

permissions:
  actions: write

jobs:
  tests:
    strategy:
      matrix:
        ddev_version: [stable, HEAD]
      fail-fast: false

    runs-on: ubuntu-latest

    steps:
      - uses: ddev/github-action-add-on-test@v2
        with:
          ddev_version: ${{ matrix.ddev_version }}
          token: ${{ secrets.GITHUB_TOKEN }}
          debug_enabled: ${{ github.event.inputs.debug_enabled }}
          addon_repository: ${{ env.GITHUB_REPOSITORY }}
          addon_ref: ${{ env.GITHUB_REF }}
```

## License

[Apache](LICENSE)

## Contribute

Anyone is welcome to submit a pull request to this repository.

For more details on development processes, please read the [developer guide](./docs/DEVELOPER.md).

**Contributed and maintained by [julienloizelet](https://github.com/julienloizelet)**
