# robloxctl

A terminal-style controller for your own Roblox account. Send friend requests, follow users, manage incoming requests, look up profiles, and join games — all from a command line.

- **Closed source.** This repository contains **no source code**, only documentation. Prebuilt binaries are attached to [Releases](../../releases/latest).
- Windows only. Requires Python-free standalone `robloxctl.exe`.

## Features

| Command | What it does |
|---|---|
| `login [cookie]` | authenticate with your `.ROBLOSECURITY` cookie (saved locally) |
| `logout` | forget the saved cookie |
| `me` | show your account info |
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
| `game <place\|url>` | game info (name, visits, creator) |
| `join <place\|url>` | open a game in your browser — **no Roblox client needed** |
| `update` | self-update to the newest release from GitHub |
| `version` | show your version and the latest release |
| `help` / `exit` | list commands / leave |

Users can be given as a username (`Builderman`) or a numeric id (`1`).

## Install

1. Download `robloxctl.exe` from the latest [release](../../releases/latest).
2. Run it — an interactive terminal opens. Or run one-off commands:
   ```
   robloxctl.exe join 4483381587
   robloxctl.exe friend Builderman
   ```

## First run (get your cookie)

1. Open [roblox.com](https://www.roblox.com) and log into the account you want to control.
2. Press `F12` → **Application** → **Cookies** → `roblox.com` → copy the value of `.ROBLOSECURITY`.
3. In the tool: `login` and paste it.

The cookie is stored in `%APPDATA%\robloxctl\cookie` (hidden) and is **never** sent to or shared with anyone other than Roblox itself.

## Joining games without the Roblox client

Roblox normally requires its desktop client. This tool does not launch or depend on the local client — instead `join` opens the game page in your default browser and prints the launcher link, so Roblox handles the actual join on its side.

## Updating

robloxctl checks for a newer release every time it starts and prints a notice when one exists. Run `update` to download and install it (or `robloxctl.exe --update`). The new version replaces the old exe automatically and restarts.

## Legal / disclaimer

- Use this only on accounts you own.
- Automating accounts may breach the Roblox Terms of Use; use at your own risk.
- Your cookie is a login credential — treat it like a password and never share it.

No source code is published. Binaries are distributed via GitHub Releases only.