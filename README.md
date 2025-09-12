# setup-codeql

A GitHub Action for running [CodeQL binaries](https://github.com/github/codeql-cli-binaries).

# Using

This action installs a CodeQL binary and any packs found in your repository (as identified by a directory containing `codeql-pack.lock.yml`). These assets are then cached for improved performance.

Usage will look something like this:

```yaml
on:
  pull_request:
  push:
    branches: [main]

jobs:
  main:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - uses: trailofbits/setup-codeql@main
        with:
          version: '2.23.0'
          platform: 'linux64'
          checksum: 'b5dec48ca1848cec8323816414830ea87edd3178ef5686c71946020a36cd5a61'
      - run: codeql --version
```

Or omit everything under `with` to use the defaults.

This is particularly useful for running query tests in CI:

```yaml
...
steps:
  - uses: actions/checkout@v5
  - uses: trailofbits/setup-codeql@main
  - name: Run tests
    run: codeql test run --threads=0 /path/to/query/tests
```
