# Branch: custom

Integration branch that merges all feature branches onto `main`.

## Current Phase

Stable. All features implemented, compiled, pushed to origin.

## Features

### 1. Transient Auto-Selection (`feat/transient-auto-selection`)
- Chip in message editor showing current code selection as transient context
- Auto-focus: when agent panel is open, selecting code auto-inserts context
- `auto_focus_on_selection` setting (default: true)
- `ctrl+cmd+a` toggle action (`ToggleAutoFocusOnSelection`)

### 2. Token Usage Display (`feat/token-usage-display`)
- Wires `ACP UsageUpdate` into `TokenUsage` struct
- Preserves larger context window (`max_tokens.max(usage.size)`) to avoid 200k overwrite on 1M models
- Compact mode: circular progress ring
- Detailed mode: percentage + used/max labels
- Click to toggle between modes
- `context_window_display` setting (Compact/Detailed)

### 3. Multi-Tab Agent Panel (`feat/multi-tab-panel`)
- Tab bar in agent panel (max 9 tabs)
- `cmd+1` through `cmd+9` to switch tabs
- `ctrl+w` to close current tab
- Idle tab eviction when max reached
- Background threads retained when tabs close

## Tasks

| # | Task | Status | Agent |
|---|---|---|---|
| — | All features implemented | Done | — |

## Last Updated

2026-04-03
