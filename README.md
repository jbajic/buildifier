# buildifier action

![verify-run-buildifier.yml](https://github.com/jbajic/buildifier/actions/workflows/verify-run-buildifier.yml/badge.svg?event=schedule)

GitHub Action for running Bazel's build tool buildifier. Works on linux, macOS
and windows.

Buildifier automatically checks one of the Bazel's files:
 - `BUILD`
 - `WORKSPACE`
 - `.bzl`

## Inputs


| Name  | Description | Required | Default |
| --- | --- | --- | --- |
| version  | The version of the used `buildifier` | `false`| `5.1.0` |
| path  | The path on which to run buildifier check. | `false`| `.` |
| mode  | The mode in which to run buildifier <code>[check&#124;diff]</code> | `false` | `check` |

## Example Usage

To use `buildifier` action you can follow presented examples to see how it works:

### Check every file
```yml
name: Bazel files check
on: [push]
jobs:
  formatting-check:
    name: Run buildifier check
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3

    - name: Run buildifier
      uses: jbajic/buildifier@v1
```

### Check files in `src` directory
```yml
name: Check bazel files
on: [push]
jobs:
  formatting-check:
    name: Run buildifier check
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3

    - name: Run buildifier
      uses: jbajic/buildifier@v1
      with:
        path: src
```

### Check all Bazel files and print out the difference
```yml
name: Check bazel files
on: [push]
jobs:
  formatting-check:
    name: Run buildifier check
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3

    - name: Run buildifier
      uses: jbajic/buildifier@v1
      with:
        path: src
        mode: diff
```

To print out the diff two steps will be performed:
 1. Run buildifier in `multi_diff` mode,
 2. Run `git diff` and print out the changes.

## License

Apache-2.0
