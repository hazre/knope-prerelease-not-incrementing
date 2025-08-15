# Knope Prerelease Version Increment Bug Repro

This repository reproduces an issue with [Knope](https://github.com/knope-dev/knope) not incrementing prerelease versions correctly.

## Environment

* **OS:** Windows 11 Pro 10.0.26100
* **Knope:** 0.21.2 (installed via `cargo binstall knope`)

## Problem

When running a prerelease command, Knope bumps the version from `1.0.0-rc.0` to
`0.0.1-rc.0` instead of the expected `1.0.0-rc.1`.

## Steps to Reproduce

1. Clone this repository.
2. Run either of the following commands:

   ```bash
   knope release --dry-run --verbose --prerelease-label rc
   ```

   or

   ```bash
   knope pre-release --dry-run --verbose
   ```

## Sample Output

```
knope pre-release --dry-run --verbose
Loading package
package.json has version 1.0.0-rc.0
Looking for Git tags matching package name.
Running step BumpVersion(Pre { label: Label("rc"), stable_rule: Patch })
Pre-release label rc selected. Determining next stable version...
Using PATCH rule to bump from 0.0.0 to 0.0.1
No existing pre-release version found; creating rc.0
Would add the following to package.json: version = 0.0.1-rc.0
Running step PrepareRelease(PrepareRelease { prerelease_label: None, allow_empty: false, ignore_conventional_commits: true })
changeset initial_change.md
        implies rule PATCH
Using PATCH rule to bump from 0.0.0 to 0.0.1
Would delete .changeset\initial_change.md
Would add files to git:
  .changeset/initial_change.md
```