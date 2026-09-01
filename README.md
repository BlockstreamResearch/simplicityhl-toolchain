# SimplicityHL toolchain

This action installs precompiled [Simplex][1]
and [Simfmt][2] binaries. It does not
install, select, or modify Rust or Cargo.

## Usage

Set up the Rust version required by your project separately, then select the
SimplicityHL components to install:

```yaml
steps:
  - uses: actions/checkout@v6

  - name: Install Rust
    uses: dtolnay/rust-toolchain@stable
    with:
      toolchain: "1.91.0"

  - id: toolchain
    name: Install SimplicityHL tools
    uses: BlockstreamResearch/simplicityhl-toolchain@v1
    with:
      components: simplex@0.0.10,simfmt@0.0.2

  - run: simplex --version
  - run: simfmt --version
```

For security-sensitive workflows, pin actions to the full commit SHA of the
release you reviewed instead of a movable tag.

## Inputs

### `components`

Required. A comma-separated list containing `simplex`, `simfmt`, or both. Add
`@VERSION` to an entry to install a specific release:

```yaml
components: simplex,simfmt
components: simplex@0.0.10
components: simplex@v0.0.10,simfmt@0.0.2
```

An entry without a version resolves the latest stable release. Empty entries,
unknown components, duplicates, and malformed versions are rejected.

## Outputs

| Output | Description |
| --- | --- |
| `simplex-version` | Installed Simplex version, or empty if it was not selected. |
| `simfmt-version` | Installed simfmt version, or empty if it was not selected. |

```yaml
- id: toolchain
  uses: BlockstreamResearch/simplicityhl-toolchain@v1
  with:
    components: simplex,simfmt

- run: printf '%s / %s\n' "$SIMPLEX_VERSION" "$SIMFMT_VERSION"
  env:
    SIMPLEX_VERSION: ${{ steps.toolchain.outputs.simplex-version }}
    SIMFMT_VERSION: ${{ steps.toolchain.outputs.simfmt-version }}
```

## Precompiled binaries only

* Simplex is installed through `simplexup`. 
* Simfmt is installed by the standalone
precompiled `cargo-binstall` executable with only its official crate-metadata release strategy enabled.

Supported platforms are determined by each project's published release assets.
The action does not maintain a separate architecture table. See the
[Simplex releases][3] and [Simfmt releases][4].

## Development and releases

After checking out this repository, workflows can test the unpublished action
with `uses: ./`. The action implementation is the root `install` script; the
separate `.github/scripts/simfmt-check` helper is used only for repository
format checks.

[1]: https://github.com/BlockstreamResearch/smplx
[2]: https://github.com/BlockstreamResearch/simfmt
[3]: https://github.com/BlockstreamResearch/smplx/releases
[4]: https://github.com/BlockstreamResearch/simfmt/releases