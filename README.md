# DDEV add-on test init


A GitHub Action to initialize DDEV add-on tests.


<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

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
- uses: julienloizelet/ddev-add-on-test@v0.3.0
  with:
    ddev_version: "stable"
```

This step will install the latest stable version of DDEV.

In the steps that follow, you will be able to run any DDEV commands.


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

If enabled, action will use [keepalive-workflow action](gautamkrishnar/keepalive-workflow) when `ddev_version` has 
been set to `stable`.

**N.B.** If enabled, you have to update the permission of the main workflow to `write`:

```yaml
permissions:
  contents: write
```

Not required.

Default: `true`.

---


- `keepalive_time_elapsed` (_String_)

Time elapsed from the previous commit to trigger a new automated commit (in days).

Will be used as the `time_elapsed` key of the  [keepalive-workflow action](gautamkrishnar/keepalive-workflow)

Not required.

Default: `55`.

---


- `debug_enabled` (_Boolean_)

If `true`, a tmate session will be accessible before the tests step. See [action-tmate](https://github.com/mxschmitt/action-tmate) for more details.

Not required.

Default: `false`.

---


- `token` (_String_)

A GitHub Personal Access Token used by the `debug` and `run test` steps.

Required.

Example: `${{ secrets.GITHUB_TOKEN }}`.

---


## Usage

### Test your DDEV add-on

If your add-on is based on the [DDEV add-on template repository](https://github.com/ddev/ddev-addon-template), you 
should have a tests folder containing a `test.bats` file.

Using this GitHub action, a  `.github/workflows/tests.yml` file could have the following content: 


```yaml
name: tests
on:
  pull_request:
  push:
    branches: [ main ]
    paths-ignore:
      - '**.md'

  schedule:
  - cron: '25 08 * * *'

  workflow_dispatch:
    inputs:
      debug_enabled:
        type: boolean
        description: Debug with tmate
        default: false

permissions:
  contents: write


jobs:
  tests:

    strategy:
      matrix:
        ddev_version: [stable, HEAD]
      fail-fast: false

    runs-on: ubuntu-20.04

    steps:


    - uses: julienloizelet/ddev-add-on-test@v0.3.0
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


**Contributed and maintained by [julienloizelet](https://github.com/julienloizelet)**
