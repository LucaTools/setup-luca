# setup-luca

GitHub Action for installing [Luca](https://luca.tools) — the lightweight CLI tool manager — and optionally installing the tools defined in a spec file.

---

## Usage

### Minimal — install Luca CLI only

```yaml
- uses: LucaTools/setup-luca@v1
```

### Full setup — install Luca CLI and tools

```yaml
- uses: LucaTools/setup-luca@v1
  with:
    spec: Lucafile
```

### Pin a specific Luca version

```yaml
- uses: LucaTools/setup-luca@v1
  with:
    version: "1.2.3"
    spec: Lucafile
```

---

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `version` | Luca version to install (e.g. `"1.2.3"`). Omit to use the latest release. | No | `""` (latest) |
| `spec` | Path to the Luca spec file, relative to the workspace root. Omit to skip tool installation. | No | `""` (skip) |

When `spec` is provided, all tools listed in the spec file are added to `PATH` and available by name in subsequent steps.

---

## Full workflow example

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: macos-latest

    steps:
      - uses: actions/checkout@v4

      - uses: LucaTools/setup-luca@v1
        with:
          spec: Lucafile

      - run: swiftlint --version
      - run: tuist version
```

---

## Versioning

Actions follow [semantic versioning](https://semver.org). A floating major tag (`v1`, `v2`, …) is always updated to point to the latest release within that major version. Pinning to a major tag (e.g. `@v1`) is recommended for most workflows — you will receive non-breaking updates automatically.

To pin to an exact release use the full tag (e.g. `@v1.2.3`).

---

## License

[Apache 2.0](LICENSE)
