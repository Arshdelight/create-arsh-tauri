# create-arsh-tauri

[![npm version](https://img.shields.io/npm/v/create-arsh-tauri)](https://www.npmjs.com/package/create-arsh-tauri)

The lightweight desktop stack we use for client work, one command away: **Tauri 2 + Vite + React 19 + TypeScript + Tailwind CSS 4**, a frameless window with a hand-rolled title bar, the same UI kit as `create-arsh-electron` — and Rust-side release polish (LTO, strip) done at the factory level.

```bash
npm create arsh-tauri@latest my-app
```

## What you get

```
├── src-tauri/           # Rust backend: commands, window config, bundle settings
├── src/                 # frontend (React + Tailwind 4)
│   └── ui/              # AppLayout, TitleBar, NavItem, Button, Dialog,
│   │                    # Tooltip, Spinner, Switch — theme tokens in
│   │                    # plain CSS variables, same kit as arsh-electron
├── AGENTS.md            # bootstrap: the first AI session interviews you
│                        # and writes this project's conventions
├── src-tauri/tauri.conf.json
└── vite.config.ts
```

- **Frameless window, custom title bar** — minimize / maximize / close via Tauri's window API, double-click to toggle maximize, an optional always-on-top pin, drag regions already wired up
- **Minimal single-page starter** — a counter button plus a `greet` round-trip through Rust, so the bridge is proven before you write real code
- **Test & CI baseline** — vitest wired up (`npm test`), a GitHub Actions workflow running lint + typecheck + tests + `cargo check` on push/PR
- **Packaging polish built in** — release profile with LTO + strip for small binaries, fixed Vite dev port (1420) that the Tauri CLI expects, a complete `.gitignore`, and git initialized with a first commit so AI edits are diffable from day one
- **Tiny output** — a scaffolded app builds to a few MB, no bundled runtime browser

## Usage

```bash
npm create arsh-tauri@latest [project-name]
npm create arsh-tauri@latest [project-name] -- --scope <name>

# non-interactive
npm create arsh-tauri@latest my-app -- --yes
```

| Flag | Description |
|---|---|
| `--scope <name>` | bundle identifier namespace, `com.<scope>.<app>` (default: `arshdelight`) |
| `--yes` | Skip prompts, use defaults (git init included) |

The CLI asks two questions — project name, git init or not — and derives everything else: `package.json` name (and `author`, from your git config), Rust crate + lib names, bundle `identifier`, `productName`, window title and title-bar brand. Answer `arsh-demo` and you get crate `arsh-demo`, lib `arsh_demo_lib`, product `ArshDemo` / `com.arshdelight.arshdemo`; add `--scope mycompany` and it becomes `com.mycompany.arshdemo`.

## Prerequisites

- Node.js ≥ 20.11
- Rust ≥ 1.77.2 (`rustup` — https://rustup.rs)
- WebView2 (preinstalled on Windows 10/11) — see https://tauri.app/start/prerequisites/

## License

MIT
