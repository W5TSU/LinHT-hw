# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

KiCad hardware design for LinHT, an open-source Linux SDR handheld (CompuLab MCM-iMX93 SoM + Semtech SX1255 direct-IQ front-end), built as a replacement mainboard for a Retevis C62 donor radio. There is no firmware or software here; the Yocto layers live in separate `meta-linht-*` repos. `main` is Rev C (unvalidated, unmanufactured); `revA` / `revB` tags are historical snapshots. Record hardware changes per revision in `CHANGELOG.md` under `[Unreleased] - Revision C`.

## Build

`make` builds everything into `build/` (fabrication files land in `build/web/files/`). Individual targets: `render`, `models`, `fabrication`, `side-fabrication`, `web`, `clean`.

- The design files are **KiCad 10 format** (`version 20260206`). A local KiCad 9 `kicad-cli` cannot open them. `make` also needs `kikit`, `xsltproc`, `jinja2` (jinja2-cli), and `python3 -m markdown`.
- CI (`.github/workflows/main.yml`) runs plain `make` inside `ghcr.io/slintak/kicad-builder:latest` on every push and deploys `build/web/` to GitHub Pages from `main`. That container is the reference toolchain.
- Gerbers come from the **kikit panel** (`panel.json`: v-cuts, 11 mm frame, fiducials, tooling holes), not the bare board. `kikit fab` runs with `--no-drc`, so the build never catches DRC errors; check DRC in KiCad yourself.
- `kicad-cli pcb export step` exit code 2 (missing 3D models) is tolerated deliberately.

## Design structure

- `linht-hw.kicad_sch` is the root sheet; its sub-sheets are `soc`, `power`, `rf`, `audio`, `gnss`, `display`, `keyboard`, `connectors`. `mux.kicad_sch` is **not referenced** by the root sheet and is not part of the design.
- `linht-hw.kicad_pcb` is ~21 MB; read it with targeted `grep`, not whole-file reads.
- Project-local libraries resolve via `${KIPRJMOD}` through `sym-lib-table` / `fp-lib-table`: symbols in `parts/*.kicad_sym` (general ones in `parts/parts.kicad_sym`), footprints in `parts/parts.pretty/`, 3D models in `parts/parts.3dshapes/`.
- `side-pcb/` is a separate KiCad project (side-button board, soldered edge-on to the main PCB, outline matches the C62 original). Built by `make side-fabrication` with `kikit fab jlcpcb`, unpanelized.
- `mcm-imx93-pinout.md` maps SoM pins to LinHT net names and voltage domains; keep it in sync when changing SoM connections in `soc.kicad_sch`.

## Part fields and BOM

- The JLCPCB BOM CSV is produced by `present/bom2grouped_csv_jlcpcb.xsl`, which reads only the `LCSC` and `PN` symbol fields. Parts lacking them come out incomplete in the BOM.
- Symbols also carry `Mouser` / `Mouser Part Number` and `MPN`; Rev C Mouser numbers are complete, and `mouser-order-notes.md` lists the new Rev C parts to order.

## Web page

`present/template/index.html.j2` is rendered with `present/template/index.json` and includes `README.html` (converted from `README.md`), so the README is the published landing page. Every file in `index.json`'s `files` list must be a real output in `build/web/files/`; add an entry there when you add a fabrication output. (`linht-hw_bom.txt` is listed but no Makefile rule produces it.)
