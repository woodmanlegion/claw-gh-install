# claw-gh-install

Install OpenClaw plugins and skills directly from GitHub — no npm publishing required.

## Binary locations

| Path | What it is |
|------|-----------|
| `bin/claw-gh-install` | Source binary inside this skill (installed to `~/.openclaw/workspace/skills/claw-gh-install/bin/`) |
| `~/.openclaw/workspace/bin/claw-gh-install` | Symlink on the gateway PATH — this is what agents and the shell use |

The symlink is created automatically at install time and points to the tmp clone binary, which stays current across `--update` calls.

## Bootstrap install

Since `claw-gh-install` can't install itself, the first install is manual:

```bash
git clone https://github.com/woodmanlegion/claw-gh-install \
  ~/.openclaw/workspace/claw-gh/tmp/claw-gh-install
openclaw skills install ~/.openclaw/workspace/claw-gh/tmp/claw-gh-install
ln -sf ~/.openclaw/workspace/skills/claw-gh-install/bin/claw-gh-install \
  ~/.openclaw/workspace/bin/claw-gh-install
```

After that, updates are self-managed:
```bash
claw-gh-install --update claw-gh-install
```

## Usage

```bash
claw-gh-install woodmanlegion/termux-sms-channel   # install plugin
claw-gh-install woodmanlegion/skill-sms-send        # install skill
claw-gh-install --update termux-sms-channel         # update
claw-gh-install --list                              # list installed
claw-gh-install --remove termux-sms-channel         # remove
claw-gh-install --show-config                       # show paths
```
