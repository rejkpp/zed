# Zed (Custom Fork)

Personal fork of [Zed](https://github.com/zed-industries/zed) with Agent Thread UI enhancements.

## Custom Features

### Multi-Tab Agent Panel
Multiple agent conversations in tabs. `cmd+1-9` to switch, `ctrl+w` to close. Max 9 tabs with idle eviction.

### Token Usage Display
Live token usage in the thread toolbar. Compact (progress ring) or detailed (percentage + counts) — click to toggle. Setting: `context_window_display`.

### Transient Auto-Selection Context
Code selections auto-appear as context chips in the agent message editor. `ctrl+cmd+a` to toggle. Setting: `auto_focus_on_selection`.

## Branch Structure

```
main                              (upstream mirror — no custom commits)
├── feat/transient-auto-selection (context chip + auto-focus + toggle)
├── feat/token-usage-display      (usage wiring + inline labels + display toggle)
└── feat/multi-tab-panel          (tabs + keyboard shortcuts)

custom = main + all feat branches merged
```

Each feature lives on its own branch. This means:
- **Conflicts are resolved per-feature** during upstream sync
- **Features can be dropped** if upstream ships equivalent functionality
- **New features** are added as new branches and merged into `custom`

## Upstream Sync

```bash
git fetch upstream
git checkout main && git pull upstream main

# Rebase each feature onto updated main
git checkout feat/transient-auto-selection && git rebase main
git checkout feat/token-usage-display && git rebase main
git checkout feat/multi-tab-panel && git rebase main

# Rebuild custom from scratch
git checkout custom && git reset --hard main
git merge feat/transient-auto-selection --no-edit
git merge feat/token-usage-display --no-edit
git merge feat/multi-tab-panel --no-edit

# Push
git push --force-with-lease origin custom feat/transient-auto-selection feat/token-usage-display feat/multi-tab-panel
```

To drop a feature, simply omit its branch from the merge sequence and delete it.

---

# Zed

[![Zed](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/zed-industries/zed/main/assets/badge/v0.json)](https://zed.dev)
[![CI](https://github.com/zed-industries/zed/actions/workflows/run_tests.yml/badge.svg)](https://github.com/zed-industries/zed/actions/workflows/run_tests.yml)

Welcome to Zed, a high-performance, multiplayer code editor from the creators of [Atom](https://github.com/atom/atom) and [Tree-sitter](https://github.com/tree-sitter/tree-sitter).

---

### Installation

On macOS, Linux, and Windows you can [download Zed directly](https://zed.dev/download) or install Zed via your local package manager ([macOS](https://zed.dev/docs/installation#macos)/[Linux](https://zed.dev/docs/linux#installing-via-a-package-manager)/[Windows](https://zed.dev/docs/windows#package-managers)).

Other platforms are not yet available:

- Web ([tracking issue](https://github.com/zed-industries/zed/issues/5396))

### Developing Zed

- [Building Zed for macOS](./docs/src/development/macos.md)
- [Building Zed for Linux](./docs/src/development/linux.md)
- [Building Zed for Windows](./docs/src/development/windows.md)

### Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for ways you can contribute to Zed.

Also... we're hiring! Check out our [jobs](https://zed.dev/jobs) page for open roles.

### Licensing

License information for third party dependencies must be correctly provided for CI to pass.

We use [`cargo-about`](https://github.com/EmbarkStudios/cargo-about) to automatically comply with open source licenses. If CI is failing, check the following:

- Is it showing a `no license specified` error for a crate you've created? If so, add `publish = false` under `[package]` in your crate's Cargo.toml.
- Is the error `failed to satisfy license requirements` for a dependency? If so, first determine what license the project has and whether this system is sufficient to comply with this license's requirements. If you're unsure, ask a lawyer. Once you've verified that this system is acceptable add the license's SPDX identifier to the `accepted` array in `script/licenses/zed-licenses.toml`.
- Is `cargo-about` unable to find the license for a dependency? If so, add a clarification field at the end of `script/licenses/zed-licenses.toml`, as specified in the [cargo-about book](https://embarkstudios.github.io/cargo-about/cli/generate/config.html#crate-configuration).

## Sponsorship

Zed is developed by **Zed Industries, Inc.**, a for-profit company.

If you’d like to financially support the project, you can do so via GitHub Sponsors.
Sponsorships go directly to Zed Industries and are used as general company revenue.
There are no perks or entitlements associated with sponsorship.
