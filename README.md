# SimplicityHL toolchain

This action installs a precompiled [Simplex][1] toolchain. It does not install,
select, or modify Rust or Cargo.

## Usage

Set up the Rust version required by your project separately. With no component
input, the action installs the latest stable Simplex release:

```yaml
steps:
  - uses: actions/checkout@v6

  - name: Install Rust
    uses: dtolnay/rust-toolchain@stable
    with:
      toolchain: "1.91.0"

  - id: toolchain
    name: Install SimplicityHL tools
    uses: BlockstreamResearch/simplicityhl-toolchain@v0.0.3

  - run: simplex --version
  - run: simplex fmt --check
```

For security-sensitive workflows, pin actions to the full commit SHA of the
release you reviewed instead of a movable tag.

## Inputs

### `components`

Optional. A comma-separated component list that currently supports `simplex`.
Add `@VERSION` to install a specific release:

```yaml
components: simplex
components: simplex@0.0.13
components: simplex@v0.0.13
```

Omitting the input, or passing an empty or whitespace-only value, installs the
latest stable Simplex release. Empty entries within a non-empty list, unknown
components, duplicates, and malformed versions are rejected.

## Outputs

| Output | Description |
| --- | --- |
| `simplex-version` | Installed Simplex version. |

```yaml
- id: toolchain
  uses: BlockstreamResearch/simplicityhl-toolchain@v0.0.3
  with:
    components: simplex@0.0.13

- run: printf 'Simplex %s\n' "$SIMPLEX_VERSION"
  env:
    SIMPLEX_VERSION: ${{ steps.toolchain.outputs.simplex-version }}
```

## Precompiled binaries only

Simplex is installed through `simplexup`.

Supported platforms are determined by the published Simplex release assets.
The action does not maintain a separate architecture table. See the
[Simplex releases][2].

[1]: https://github.com/BlockstreamResearch/smplx
[2]: https://github.com/BlockstreamResearch/smplx/releases
