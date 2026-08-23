# Loadstone Registry

The community package registry for [Loadstone Mod Manager](https://github.com/bradjrenshaw/loadstone),
a unified, accessible mod manager built for game accessibility mods — one
signed manager (or per-mod installer) instead of a hand-rolled installer per
mod.

Every file in [`loadstone-packages/`](loadstone-packages/) is a package:

- **Link files** point at a mod's own repository, which carries its full
  manifest and game data in its own `loadstone-packages/` directory. Listing
  a mod here is a one-time pull request; releases and fixes never touch this
  repo again.
- **Full package files** are hosted here directly — shared tools like a mod
  loader, pinned to exact upstream release assets by SHA-256.

## Using this registry

With the `loadstone` CLI:

```
loadstone install blindfold --registry github:bradjrenshaw/loadstone-registry
```

Or pin it in a distribution profile (`loadstone.json` next to the
executable, or embedded in a branded installer build):

```json
{ "registries": ["github:bradjrenshaw/loadstone-registry"] }
```

## Listing your mod

1. Add a `loadstone-packages/` directory to your mod's repository containing
   your mod's manifest and (usually) the game package it targets — see the
   [format specification](https://github.com/bradjrenshaw/loadstone) and its
   worked examples.
2. Attach a generated `release.json` to each GitHub release
   (`loadstone package` does this from your build script).
3. Open a pull request here adding one link file:

```json
{
  "kind": "link",
  "source": "github:you/your-mod",
  "packages": ["your-mod-id"]
}
```

Review vouches that the link points at the real author's repository; each
release is then trusted to that author's GitHub account, exactly like
downloading from their releases page today.

## What's listed

- `blindfold` — screen-reader accessibility for Balatro
- `lovely-injector` — runtime Lua injector (tool; registry-pinned to
  upstream releases with audited hashes)
