# robloxctl

A controller for your own Roblox accounts. Send friend requests, follow users, manage accounts, join games locally (with multi-account, multi-instance support), and self-update — all wrapped in a modern dark desktop app.

- **Closed source.** This repository contains **no source code**, only documentation. Prebuilt binaries are attached to [Releases](../../releases/latest).
- Windows only. Requires the standalone `robloxctl.exe`.

## Interface

Running `robloxctl.exe` opens a **dark desktop window** (no terminal):

- **Account** — shows who you're logged in as; **Log in** opens a paste-your-cookie form, **Log out** clears it.
- **Quick actions** — friend / follow, search a user, or join a game with two clicks.
- **Sidebar** — `Me`, `Friend requests`, `My friends`.
- **Command bar** — type any command from the table below (arrow keys recall history).

Prefer the terminal? Every command works the old way too:

| Flag | What it does |
|---|---|
| `--cli` | open the interactive terminal (old style) |
| `--cmd <line>` | run a single command and exit quietly (used internally by the GUI) |
| `--check` | print the update status as a machine-readable line |
| `--update` | silently install the newest release and exit |
| `--restart` | relaunch the current exe (used by the updater) |
| `--no-update-check` | skip the background update check |
| `--version` | print the version and exit |

## Features

| Command | What it does |
|---|---|
| `login [cookie]` | authenticate with your `.ROBLOSECURITY` cookie (saved locally) |
| `logout` | forget the saved cookie |
| `me` | show your account info |
| `acct list` | list saved accounts |
| `acct add <name>` | save another account's cookie as a profile |
| `acct use <name>` | switch the active account |
| `acct del <name>` | delete a profile |
| `id <user>` | resolve a username to an account id |
| `user <user>` | full public profile (counts, description, created) |
| `search <query>` | search users |
| `friend <user>` / `unfriend <user>` | send / remove a friend request |
| `follow <user>` / `unfollow <user>` | follow / unfollow |
| `requests` | list incoming friend requests |
| `accept <user\|all>` | accept incoming friend request(s) |
| `decline <user\|all>` | decline incoming friend request(s) |
| `friends [user]` | list friends (yours or a user's) |
| `presence <user>` | online / in-game / studio status |
| `avatar <user>` | avatar assets and body scales |
| `game <place\|url>` | game info (name, builder, price, url) |
| `join <place\|url>` | join the game **in your Roblox client — no browser** |
| `update` | show the update window (what's new + Update now / Later) |
| `version` | show your version and the latest release |
| `help` / `exit` | list commands / leave |

Users can be given as a username (`Builderman`) or a numeric id (`1`).

## Install

1. Download `robloxctl.exe` from the latest [release](../../releases/latest).
2. Double-click it — the robloxctl window opens. Or run one-off commands:
   ```
   robloxctl.exe join 4483381587
   robloxctl.exe friend Builderman
   ```

## First run (get your cookie)

1. Open [roblox.com](https://www.roblox.com) and log into the account you want to control.
2. Press `F12` → **Application** → **Cookies** → `roblox.com` → copy the value of `.ROBLOSECURITY`.
3. In the app: click **Log in** and paste it, or type `login` in the command bar.

Cookies are stored under `%APPDATA%\robloxctl` (hidden) and are **never** sent to anyone other than Roblox.

## Joining games locally

`join` launches the game directly in your installed Roblox client — no browser involved:

1. It finds your client automatically (`RobloxPlayerBeta.exe` under `Roblox`, `Voidstrap`, or `Bloxstrap` installs, or the registered `roblox-player` protocol handler).
2. It mints a short-lived **auth ticket** for the active account.
3. It builds the official launch URI and hands it straight to the client binary.

```
robloxctl.exe join 4483381587
```

### Multi-account & multi-instance

Run several Roblox clients at once, one per saved account, each joining as its own ticket (spawns the client directly with `-secondinst` so multiple instances run side by side):

```
robloxctl.exe join 189707 -a alt1 -a alt2 -a main
```

Add extra same-account instances with `-n`:

```
robloxctl.exe join 189707 -a alt1 -n 2
```

Test without launching anything (builds the URLs and prints them):

```
robloxctl.exe join 189707 --dry
```

Note: each instance plays as the account whose cookie minted its ticket. Multi-instance launching relies on Roblox-internal behavior and can break when Roblox updates.

## Updating

Every time robloxctl starts it checks GitHub for a newer release. If one exists:

1. It quietly downloads and installs the new exe **in the background** (no prompts, no interruption).
2. A dark window then tells you it's ready:
   - **Restart now** — launches the updated exe right away.
   - **Later** — keeps working in the current session; the new version starts next launch.

You can trigger the same flow manually anytime with `update`, or update silently and exit with `robloxctl.exe --update`. Use `--no-update-check` to skip the background check.

**Updating from v0.1.0 or v0.2.0:** those builds only replace the exe after the
process has exited, so trigger the update as a *one-shot* command and let the
window close — do **not** run `update` from the interactive prompt (the terminal
would wait forever in v0.1.0). From a terminal:

```
robloxctl.exe --update
```

Starting with v0.2.1 the updater can swap the exe while the program is still
running, so `update` works from inside the app too.

## Legal / disclaimer

- Use this only on accounts you own.
- Automating accounts — and multi-instance launching — may breach the Roblox Terms of Use; use at your own risk.
- Your cookie is a login credential — treat it like a password and never share it.

No source code is published. Binaries are distributed via GitHub Releases only.