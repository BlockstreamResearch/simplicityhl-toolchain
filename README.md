# SimplicityHL toolchain


This action installs precompiled [Simplex][1] and [Simfmt][2] binaries. It does not install, select, or modify Rust or Cargo.

This action installs a precompiled [Simplex][1] toolchain. Simplex releases starting with `v0.0.11` include the matching [Simfmt][2] binary, so both tools are installed from one reproducible release. The action does not install, select, or modify Rust or Cargo.

## Usage

Set up the Rust version required by your project separately, then select the Simplex release to install:

```yaml
steps:
  - uses: actions/checkout@v7.0.1

  - name: Install Rust
    uses: dtolnay/rust-toolchain@stable
    with:
      toolchain: "1.91.0"

  - id: toolchain
    name: Install SimplicityHL tools
    uses: BlockstreamResearch/simplicityhl-toolchain@v1
    with:
      components: simplex@0.0.11

  - run: simplex --version
  - run: simfmt --version
```

For security-sensitive workflows, pin actions to the full commit SHA of the
release you reviewed instead of a movable tag.

## Inputs

### `components`

Required. Use `simplex` for the latest stable release, or add `@VERSION` to install a specific release:

```yaml
components: simplex
components: simplex@0.0.11
components: simplex@v0.0.11
```

An entry without a version resolves the latest stable release. Releases older than `v0.0.11` are rejected because they don't bundle Simfmt.

## Outputs

| Output | Description |
| --- | --- |
| `simplex-version` | Installed Simplex version. |

```yaml
- id: toolchain
  uses: BlockstreamResearch/simplicityhl-toolchain@v1
  with:
    components: simplex

- run: printf 'Simplex %s\n' "$SIMPLEX_VERSION"
  env:
    SIMPLEX_VERSION: ${{ steps.toolchain.outputs.simplex-version }}
```

## Precompiled binaries only

Simplex is installed through `simplexup`.

Supported platforms are determined by the published Simplex release assets. The action does not maintain a separate architecture table. See the [Simplex releases][3].

[1]: https://github.com/BlockstreamResearch/smplx
[2]: https://github.com/BlockstreamResearch/simfmt
[3]: https://github.com/BlockstreamResearch/smplx/releases
