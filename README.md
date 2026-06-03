# rust-cache

`rust-cache` is part of the Verzly toolchain. This repository is the public distribution surface for the tool: it provides the GitHub Action metadata, release artifacts, project-specific documentation, and the public issue surface.

The source code is maintained in the private `verzly/toolchain` workspace under `crates/rust-cache`. Keeping the source in one workspace lets the release tools share the same process, platform, artifact, checksum, and GitHub integration code without copying that infrastructure into every public repository.

## Contents

- [Source code](#source-code)
- [GitHub Action](#github-action)
- [Release artifacts](#release-artifacts)
- [Compatibility](#compatibility)
- [Contributing](#contributing)

## Source code

The Rust source for this tool lives in:

```text
verzly/toolchain/crates/rust-cache
```

This repository intentionally does not contain a `src/` directory or `Cargo.toml`. That is not an omission. The executable assets published here are built from the private source workspace and attached to this repository's own GitHub Releases.

## GitHub Action

Use the action from this repository:

```yaml
- uses: verzly/rust-cache@v1
  with:
    args: --help
```

The action downloads the matching standalone executable from `verzly/rust-cache` releases. It does not download from `verzly/toolchain`, and it does not build from source during a workflow run.

To install the binary and run it yourself in later steps:

```yaml
- uses: verzly/rust-cache@v1
  with:
    install-only: true

- run: rust-cache --help
```

## Release artifacts

Release assets are published with host-specific names:

```text
rust-cache-v1.2.3-x86_64-unknown-linux-gnu
rust-cache-v1.2.3-x86_64-apple-darwin
rust-cache-v1.2.3-x86_64-pc-windows-msvc.exe
```

Checksum files are published next to the executables when the build environment supports checksum generation.

## Compatibility

`rust-cache` is designed to be used before `cargo-release` or `tauri-release`. It owns cache routing only; it does not build release artifacts and it does not publish GitHub Releases.

The release itself is produced from `verzly/toolchain`. Pull request links in generated release notes point to that source repository, because that is where the code review history exists.

## Contributing

Issues can be opened here when the problem is specific to `rust-cache` as a user-facing tool. Source changes should be made in `verzly/toolchain` under `crates/rust-cache`.

For larger changes, keep the same rule the toolchain follows internally: each tool should own one clear responsibility and should not quietly take over another tool's job.

## License

This project is licensed under the AGPL-3.0-only license.
