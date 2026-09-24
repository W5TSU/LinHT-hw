# Rev C Parts Sourcing (5–10 boards)

Prices and stock come from the Mouser Search API, queried 2026-09-24. They go stale quickly, so re-check before ordering. The per-line data is in [`sourcing-bom.csv`](sourcing-bom.csv).

The BOM comes from the **schematic**, not the PCB. See [PCB out of sync](#pcb-out-of-sync-with-schematic).

## Totals (Mouser, spares included)

| Order | BOM lines | Parts per board | 5 boards | 10 boards |
|---|---|---|---|---|
| **Mouser: exact parts, in stock** | 45 | 116 | $466.76 | $742.49 |
| **Mouser: substitutes, in stock** | 28 | 81 | $20.43 | $29.51 |
| **Mouser: GRF5604, on backorder** | 1 | 1 | $30.10 | $45.90 |
| **Mouser total** | **74** | **198** | **$517.29** | **$817.90** |
| CompuLab: MCM-iMX93 SoM | 1 | 1 | not priced (needs a quote) | not priced |
| LCSC: J12 USB-C and L9 1 µH | 2 | 2 | not priced | not priced |
| J2 battery contact (from the C62 or JBL-EC) | 1 | 1 | $0 if salvaged | $0 if salvaged |
| **Total BOM** | **78** | **202** | | |

**Found at Mouser: 94.9% of BOM lines (74 of 78) and 98.0% of parts per board (198 of 202).** Digi-Key carries none of the four parts Mouser lacks.

Hand-fit and donor parts are not included. The SoM will probably cost more than the entire Mouser order.

**Spares rule** (sized for a consigned assembler kit; also fine for hand assembly):
- 0402/0603 passives: +10% or +10 parts, whichever is more.
- 0805/1206 passives: +10% or +5 parts, whichever is more.
- Parts under $5: +2.
- Parts $5 and up: no spares.

Each line is then rounded up to Mouser's minimum and multiple, or to the next price break if that costs less in total.

## Substitutions (need approval before the schematic is updated)

28 of 78 lines order a substitute because the schematic part can't be bought in small quantities or has no stock. The `notes` column in the CSV gives the reason for each line.

| Lines | Schematic part | Substitute ordered | Why |
|---|---|---|---|
| 20 resistor lines | UniOhm `0402WGF…` (`303-` numbers) | Yageo `RC0402FR-07…` 1%. Panasonic `ERJ-2RKF…` for 127k, 150R, 6k04 | Mouser sells UniOhm only in 10,000-piece reels, and several are out of stock |
| C44 C46 C51 C53 (10 µF 0402) | Samsung CL05A106MQ5NUNC | Yageo CC0402MPX5R5BB106 | 0 stock, 365-day lead |
| C16 C19 C36 C37 (2.2 µF 0402) | Samsung CL05A225KO5NQNC (10%) | Samsung CL05A225MO5NQNC (20%) | 0 stock |
| C68 C69 (47 nF) | Samsung CL05B473KO5NNNC | Yageo CC0402KRX7R7BB473 | 0 stock |
| C12 C66 (27 pF) | Yageo CC0402JRNPO9BN270 | Yageo AC0402JRNPO9BN270 (automotive grade) | on order only |
| C14 C55 C91 C92 (100 pF) | Murata GRM1555C1H101JA01D | Yageo CC0402JRNPO9BN101 | 0 stock |
| **C52 C54 C56 (33 pF, RF)** | Murata GJM1555C1H330**F**B01D (±1%) | Murata GJM1555C1H330**G**B01D (±2%) | 0 stock. **RF tuning part: confirm ±2% is acceptable** |
| Q1 | Vishay SI2333**DDS**-T1-BE3 | Vishay SI2333**CDS**-T1-BE3 (12 V, 5.1 A, 35 mΩ at 4.5 V, SOT-23) | 260-day lead at Mouser; 0 stock and 55-week lead at Digi-Key |

## Schematic `PN` field corrections (no part change)

| Ref | Schematic `PN` | Correct Mouser number |
|---|---|---|
| L3 | 652-SPM6530T-2R2M | 810-SPM6530T-2R2M |
| FB4 FB5 | 81-BLM21P121SG | 81-BLM21PG121SN1D |
| L6 | *(empty)*; MPN written as `XR0908SQ-23NJLC` | 994-0908SQ-23NJLC (MPN `0908SQ-23NJLC`) |
| F1 | *(empty)*; MPN `1812L200/16GR` | 576-1812L200/16DR. Same 16 V / 2 A Littelfuse part, different packaging suffix; confirm |

Other cosmetic MPN differences (hyphens, or the missing `0` in `CC402…`): R43, C26, U8. Q1's schematic value is misspelled `SI23333`.

## Open items

| Ref | Part | Status | Next step |
|---|---|---|---|
| **U7** | GRF5604 PA | **0 in stock at Mouser.** 14,870 due 2026-11-05; 51-day factory lead | Digi-Key does not carry it (API search, 2026-09-24). Backorder at Mouser now, or buy direct from Guerrilla RF |
| U1 | CompuLab MCM-iMX93-C1700D-D2-N32 | Sold only by CompuLab. Not priced | Request a quote from CompuLab for 5 or 10 units; this is likely the largest single cost |
| J12 | HRO TYPE-C-31-M-12 USB-C | Not on Mouser or Digi-Key; sold by LCSC | Buy from LCSC (tariff applies), or find a Mouser/Digi-Key part whose land pattern matches the footprint |
| L9 | SLO0520H1R0MTT 1 µH | Not on Mouser or Digi-Key; sold by LCSC | Same as J12. Compare the land pattern with `parts/parts.pretty/SLO0520H1R0MTT.kicad_mod` |

## Hand-fit and donor parts (not on the BOM)

These are fitted by the builder after assembly. Links are from [`mouser-order-notes.md`](../mouser-order-notes.md).

| Ref / item | Source |
|---|---|
| J2 battery spring contact (BT-003E, 3-way) | Salvage from the C62, or buy the [JBL-EC BT-003BE](https://www.jbl-ec.com/bt-003be-3-way-spring-battery-connector-4-1mm-pitch-smt-product/) |
| J5 display FFC, 20-pin 0.75 mm | Salvage from the C62. No distributor match found yet ([survey §7](us-fab-survey.md)) |
| J1 SMA connector | C62 donor, or [650185 on 1688](https://detail.1688.com/offer/990734696443.html) |
| J13 / J14 audio jacks (2.5 mm / 3.5 mm) | C62 donor, or AliExpress ([2.5 mm](https://www.aliexpress.com/item/32819180069.html), [3.5 mm](https://www.aliexpress.com/item/33021730474.html)) |
| SW2 volume/encoder switch | C62 donor, or [AliExpress](https://www.aliexpress.com/item/1005005183231967.html) |
| GNSS antenna pigtail (U.FL/IPEX) | [AliExpress](https://www.aliexpress.com/item/1005012352855310.html) |
| Side-button snap domes ×2 per radio | [AliExpress](https://www.aliexpress.com/item/33001419494.html) |
| Side-button PCB | `side-pcb/` Gerbers from CI |
| Display, keypad, enclosure, battery, rotary hardware | C62 donor |

## PCB out of sync with schematic

About 12 footprints in `linht-hw.kicad_pcb` carry older MPN fields than the schematic, for example L8, D4/D5, J11, R23, L7, C58, C67. The CI BOM comes from the schematic, so it is correct. Before sending pick-and-place files, run **Tools → Update PCB from Schematic** in KiCad so both files agree.
