# Deployment Decoder — PGPatcher GUID Identifier

When you run PGPatcher (ParallaxGen) with Vortex, some mods show up as
garbled names like `99_33_27_993327ba-fbfa-443c-...` instead of their real
title. That happens because PGPatcher reads mod names from Vortex's
`vortex.deployment.json`, and for some mods Vortex stores a GUID there
instead of the archive name — so you're left sorting mods you can't identify.

This tool reads that file and tells you what each GUID mod actually is.

## What it does

Drop your `vortex.deployment.json` in and it will, for every GUID-named mod:

- **Identify it** from the files it deploys (using the `PBRNifPatcher\<name>.json`
  filename, distinctive texture folders, and plugin names as fingerprints)
- **Give a verdict:**
  - 🟢 **Reinstall to fix** — a standalone Nexus mod. Remove it, manually
    download the zip, reinstall, deploy, and the name resolves. Links to Nexus.
  - 🔴 **Leave as GUID** — Community Shaders parts, collection-internal ESPs,
    SKSE `.dll` plugins, and hand-made files. These will *always* show a GUID.
    Nothing to fix — you just need to know what they are.
  - ⚪ **Needs a look** — couldn't fingerprint it confidently; shows the file
    paths so you can identify it yourself.
- **Show the top file locations** for each mod, so you can order it in
  PGPatcher by what it actually touches even if the name can't be fixed.

Filter by verdict, search by name or path.

## Privacy

Everything runs in your browser. Your deployment file is never uploaded
anywhere — the whole thing is one static HTML file with no server. You can
read the source right here to confirm that.

## How to use

1. Open the tool (link above / hosted page).
2. Find your `vortex.deployment.json` — usually in
   `...\Skyrim Special Edition\Data\`.
3. Drag it in.

## Fixing a name

Remove the mod in Vortex → manual-download the zip from its Nexus page →
reinstall → deploy → re-run PGPatcher.

## Note on coverage

The identification database is built around the **Gate to Sovngarde**
collection, so it recognises that setup's mods well. On other load orders it
will still find every GUID mod and show its file paths, but may mark more of
them "Needs a look" if it doesn't have a fingerprint for them yet.

Adding a mod is easy — each entry in the `DB` array near the top of the HTML
is one rule. PRs with new fingerprints welcome.

## Credit

Built for the Gate to Sovngarde / PGPatcher community. PGPatcher (ParallaxGen)
is by hakasapl.
