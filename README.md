<p align="center"><a href="#readme"><img src="https://gh.kaos.st/htmlcov-action.svg"/></a></p>

<br/>

Action for generating HTML files with Go coverage info using [htmlcov](https://kaos.sh/htmlcov).

### Usage

Create file `.github/workflows/htmlcov.yml`.

Add next code to it:

```yml
name: CI

on:
  push:
    branches: [master, develop]
  pull_request:
    branches: [master]

jobs:
  HTMLCov:
    name: HTMLCov
    runs-on: ubuntu-latest

    env:
      SRC_DIR: src/github.com/${{ github.repository }}

    steps:
      - name: Set up Go
        uses: actions/setup-go@v3
        with:
          go-version: '1.18.x'

      - name: Code checkout
        uses: actions/checkout@v3

      - name: Run tests
        working-directory: ${{env.SRC_DIR}}
        run: go test -coverprofile=covprofile ./...

      - name: Check scripts with Shellcheck
        uses: essentialkaos/htmlcov-action@v1
        with:
          path: ${{env.SRC_DIR}}
          profile: covprofile
```

### Options

| Option | Description | Value |
|--------|-------------|-------|
| `profile` | Path to coverage profile | _Path_ |
| `path` | Path to directory with sources | _Path_ |
| `output` | Output artifact name (_default:_ `Coverage`) | _String_ |
| `version` | Version of HTMLCov | _Version in semver notation_ |
| `retention` | Retention in days (_default:_ `3`) | _Number_ |

### License

[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0)

<p align="center"><a href="https://essentialkaos.com"><img src="https://gh.kaos.st/ekgh.svg"/></a></p>
