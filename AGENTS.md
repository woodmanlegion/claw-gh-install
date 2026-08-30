# AGENTS.md — claw-gh-install

Install OpenClaw plugins and skills from GitHub. No npm publishing required.

## When to use

When the user asks to install a plugin or skill from a GitHub repo that is
not on npm or the OpenClaw marketplace.

## First Run / Configuration

None required. Verify with:
```bash
claw-gh-install --show-config
```

If `registry_exists: false`, no repos have been installed yet — this is normal.

## Install pattern

```bash
claw-gh-install woodmanlegion/termux-sms-channel
```

After install, restart the gateway if a plugin was installed:
```bash
openclaw gateway restart
```

## Update pattern

```bash
claw-gh-install --update termux-sms-channel
openclaw gateway restart   # if plugin
```

## Routing

| Task | Command |
|------|---------|
| Install from GitHub | `claw-gh-install <owner/repo>` |
| Update installed repo | `claw-gh-install --update <name>` |
| List what's installed | `claw-gh-install --list` |
| Remove | `claw-gh-install --remove <name>` |
| Check paths | `claw-gh-install --show-config` |

## Binary location

`bin/claw-gh-install` — source binary inside the skill directory.
`~/.openclaw/workspace/bin/claw-gh-install` — symlink on PATH (created at install time).

The symlink points to the tmp clone's binary, which stays current via `git pull`.

## Framework Compatibility

| Framework | Status |
|-----------|--------|
| OpenClaw | ✅ Native |
| Pi | ✅ Compatible |
