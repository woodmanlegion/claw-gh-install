---
name: "claw-gh-install"
description: "Install OpenClaw plugins and skills from GitHub repositories. Clones to a managed tmp directory, auto-detects plugin vs skill, and symlinks binaries to the workspace PATH."
metadata:
  {
    "openclaw": {
      "emoji": "📦",
      "requires": { "bins": ["git", "openclaw"] },
      "platform": "android",
      "notes": "Requires git and openclaw CLI. Manages clones in ~/.openclaw/workspace/claw-gh/tmp/."
    }
  }
---

# claw-gh-install

Install OpenClaw plugins and skills directly from GitHub without requiring npm publishing.

## How it works

1. Clones the repo to `~/.openclaw/workspace/claw-gh/tmp/<repo-name>/`
2. Auto-detects type: plugin (has `openclaw.plugin.json`) or skill (has `SKILL.md`)
3. Runs `openclaw plugins install --force` or `openclaw skills install`
4. Symlinks user-facing binaries from `bin/` to `~/.openclaw/workspace/bin/`

## Usage

```bash
# Install a plugin or skill
claw-gh-install woodmanlegion/termux-sms-channel
claw-gh-install woodmanlegion/skill-sms-send

# Update (git pull + reinstall)
claw-gh-install --update termux-sms-channel

# List installed
claw-gh-install --list

# Remove
claw-gh-install --remove termux-sms-channel

# Show config and registry
claw-gh-install --show-config
```

## Paths

| Path | Purpose |
|------|---------|
| `~/.openclaw/workspace/claw-gh/tmp/<name>/` | Cloned repo (kept for updates) |
| `~/.openclaw/workspace/claw-gh/installed.json` | Registry of installed repos |
| `~/.openclaw/workspace/bin/<binary>` | Symlinks to skill binaries on PATH |

## Auto-detection

| Repo contains | Detected as | Install command |
|---------------|-------------|-----------------|
| `plugin/openclaw.plugin.json` | plugin | `openclaw plugins install plugin/` |
| `openclaw.plugin.json` (root) | plugin | `openclaw plugins install ./` |
| `SKILL.md` (root) | skill | `openclaw skills install ./` |

## First Run / Configuration

No configuration required. Run `claw-gh-install --show-config` to verify paths.

Requires:
- `git` — install via `pkg install git`
- `openclaw` — installed via tclaw
