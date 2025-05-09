# actions-govulncheck

A reusable GitHub Action for running [govulncheck](https://pkg.go.dev/golang.org/x/vuln/cmd/govulncheck) on Go projects. This action helps maintain code security by scanning your Go codebase for known vulnerabilities.

## Features

- Runs govulncheck on your Go codebase
- Configurable Go version
- Customizable working directory and scanning options
- Easy to integrate into your workflow
- Provides detailed feedback on security vulnerabilities
- Supports multiple analysis modes (source and binary)
- Includes test file analysis option
- Supports JSON output format
- Can analyze only imports or full function bodies
- Supports stack trace symbolization

## Usage

### Basic Usage

```yaml
name: govulncheck

on:
  pull_request: {}
  push:
    branches:
      - main
      - master

permissions:
  contents: read
  pull-requests: write

jobs:
  govulncheck:
    uses: cloudbuildlab/actions-govulncheck/.github/workflows/govulncheck.yml@v0
```

### Advanced Usage

```yaml
name: govulncheck

on:
  pull_request: {}
  push:
    branches:
      - main

permissions:
  contents: read
  pull-requests: write

jobs:
  govulncheck:
    uses: cloudbuildlab/actions-govulncheck/.github/workflows/govulncheck.yml@v0
    with:
      go-version: '1.23'
      working-directory: './cmd'
      mode: 'binary'
      include-tests: true
      json-output: true
      imports-only: false
      symbolize: true
```

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `go-version` | Go version to use | `stable` |
| `working-directory` | Working directory to run scan in | `.` |
| `mode` | Analysis mode (source or binary) | `source` |
| `tags` | Build tags to consider when analyzing source code | `` |
| `include-tests` | Include test files in analysis | `false` |
| `json-output` | Output vulnerabilities in JSON format | `false` |
| `imports-only` | Only analyze imports, not function bodies | `false` |
| `symbolize` | Symbolize stack traces in output | `false` |

## Analysis Modes

### Source Mode (Default)

- Analyzes Go source code
- Checks for vulnerabilities in dependencies
- Can analyze function bodies or just imports
- Supports build tags for conditional compilation

### Binary Mode

- Analyzes compiled binaries
- Useful for checking final artifacts
- Requires compiled binaries to be present

## Versioning

This workflow follows semantic versioning. You can use it in two ways:

1. **Major Version Tag** (Recommended):

   ```yaml
   uses: cloudbuildlab/actions-govulncheck/.github/workflows/govulncheck.yml@v0
   ```

   This will automatically use the latest release within the v0.x.x series.

2. **Specific Version**:

   ```yaml
   uses: cloudbuildlab/actions-govulncheck/.github/workflows/govulncheck.yml@v0.1.0
   ```

   This pins to a specific version for maximum stability.

### Version History

See the [Releases](../../releases) page for a full list of versions and changes.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
