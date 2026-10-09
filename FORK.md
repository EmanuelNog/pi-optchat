# Fork notes

Personal fork of [jonaslsaa/pi-optchat](https://github.com/jonaslsaa/pi-optchat).

- `origin` — this fork. Pushes go here.
- `upstream` — jonaslsaa/pi-optchat.

Local modifications, if any, live as ordinary commits on `main`; their intent is
documented in the commit messages.

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
