# Project Spec

| Field | Value |
| --- | --- |
| Project | Zed (custom fork) |
| Created | 2026-03-09 |
| Last Updated | 2026-04-03 |
| Stage | Live |

## Goals

Custom fork of the Zed editor with personal enhancements to the Agent Thread UI, rebased on top of upstream.

## Current Phase

Active — all custom features rebased onto latest upstream (synced 2026-04-02, 372 commits absorbed). Building and testing with `zed-dev`.

## Branch Strategy

Simplified rebase workflow (changed from merge-based 2026-03-21):

- **`main`** — Clean mirror of `upstream/main`. Never commit own work here.
- **`custom`** — All custom features as linear commits on top of `main`. Always build from this.

No more `feat/*` branches — all custom work lives as commits directly on `custom`.

### Upstream Sync

```bash
git fetch upstream
git checkout main && git pull upstream main
git checkout custom && git rebase main
git push --force-with-lease origin custom
```

When rebasing, resolve conflicts per commit. Check if upstream implemented similar features — drop ours if superseded.

## Build

Shell aliases (defined in `~/.zshrc`):
- `zed-dev` — Quick iteration: `git checkout custom && cargo run --release`
- `zed-bundle` — Install app bundle: `git checkout custom && ./script/bundle-mac -i`

## Custom Features (on `custom` branch)

1. **Multi-Tab Agent Panel** — Up to 9 concurrent agent threads in tabs. Tab bar auto-hides with single tab. `cmd+1`–`cmd+9` to switch, `ctrl+w` to close.

2. **Transient Auto-Selection Context Chip** — Select code in editor, auto-attaches as context chip in Agent Thread. 150ms debounce. New selection replaces old; send clears transient.

3. **Auto-Focus on Selection Toggle** — `ctrl+cmd+a` toggles whether selecting code auto-focuses the agent message input. Persists as `auto_focus_on_selection` agent setting.

4. **Token Usage Display** — Inline `5% · 49k/1M` next to progress ring. Click toggles between compact (ring only) and detailed modes. Persists as `context_window_display` setting.

5. **Context Window Fix** — Preserves model's actual context window (e.g. 1M for Opus 4.6) when ACP `UsageUpdate` reports a smaller value.

6. **UsageUpdate Wiring** — Routes ACP `UsageUpdate` notifications to token usage UI.

## Zed Configuration

User-level config in `~/.config/zed/` (persists across builds):
- `settings.json` — Theme, agent servers, dock positions, etc.
- `keymap.json` — Custom keybindings

Custom keybinding: `ctrl-cmd-c` → new thread with Claude agent (`claude-acp`).
