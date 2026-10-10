# Fork notes

Personal fork of [jonaslsaa/pi-optchat](https://github.com/jonaslsaa/pi-optchat).

- `origin` — this fork. Pushes go here.
- `upstream` — jonaslsaa/pi-optchat.

Local modifications, if any, live as ordinary commits on `main`; their intent is
documented in the commit messages.

## Local changes on `main`

- **Group-accessible modes** (`memory:` commits): directories are created
  `0o770` and files `0o660` (sockets stay `0o600`), so the machine owner's
  shared group (on pc1: human `nog` via group `agentuser`) can read/write what
  the plugin creates under `~/.optchat`. Upstream creates everything
  owner-only (`0o700`/`0o600`), which locked the human out on every new
  profile / memory generation. Runtime bridge until a pin bump picks this up:
  `~/.hermes/scripts/optchat-nog-access.sh` (mode-based `g+rwX` sweep — never
  ACLs; a POSIX ACL mask is reset by later chmods).

## Taking an upstream update (deliberately)

```sh
git fetch upstream --tags
git merge upstream/main          # or a release tag, e.g. git merge v0.9.0
npm ci && npm run check && npm test
git push origin main
```

Consumers pin this fork at a specific commit
(`git:github.com/EmanuelNog/pi-optchat@<sha>`) and bump the pin only after the
merge above passes its tests.
