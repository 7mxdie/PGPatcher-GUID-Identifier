# Deployment Decoder — PGPatcher GUID Identifier

When you run PGPatcher (ParallaxGen) with Vortex, some mods show up as
garbled names like `99_33_27_993327ba-fbfa-443c-...` instead of their real
title. That happens because PGPatcher reads mod names from Vortex's
`vortex.deployment.json`, and for some mods Vortex stores a GUID there
instead of the archive name — so you're left sorting mods you can't identify.

This tool reads that file and tells you what each GUID mod actually is.

## What it does

Drop your `vortex.deployment.json` in and, by default, it shows only the mods
that **actually appear in PGPatcher** — the ones whose coded names you really
see there. For each it will:

- **Identify it** from the files it deploys (using the `PBRNifPatcher\<name>.json`
  filename, distinctive texture folders, and plugin names as fingerprints)
- **Give a verdict:**
  - 🟢 **Reinstall to fix** — a standalone Nexus mod. Remove it, manually
    download the zip, reinstall, deploy, and the name resolves. Links to Nexus.
  - 🔴 **Leave as code** — bundled or no Nexus archive; the code is permanent
    and harmless.
  - ⚪ **Needs a look** — couldn't fingerprint it; shows file paths so you can
    identify it yourself.
- **Show the top file locations**, so you can order it in PGPatcher by what it
  actually touches even if the name can't be fixed.

### It won't over-report

Most GUID-coded entries in the file (ESP-only patches, SKSE `.dll` plugins,
Community Shaders parts) **never appear in PGPatcher at all**, so their codes
don't matter. Those are hidden by default under the **Other GUIDs** tab so you
don't panic or reinstall things you shouldn't. The headline count is only the
mods PGPatcher actually shows you.

### Finding one specific mod

Got a code in front of you in PGPatcher? Paste it (or part of it, e.g.
`99_33_27`) into the search box and it jumps straight to that mod with its real
name and verdict — searching across everything, in or out of PGPatcher.

## Privacy

Everything runs in your browser. Your deployment file is never uploaded
anywhere — the whole thing is one static HTML file with no server. You can
read the source right here to confirm that.

## How to use

1. Open the tool (the hosted page / link at the top of this repo).
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

Adding a mod is easy — each entry in the `DB` array near the top of
`index.html` is one rule. PRs with new fingerprints welcome.

## Credit

Built for the Gate to Sovngarde / PGPatcher community. PGPatcher (ParallaxGen)
is by hakasapl.
