# US Fab + Assembly Survey: LinHT Rev C, qty 5

Access date for every citation: **2026-09-24** (all URLs were accessed on that date). Bracketed numbers such as [S12] point to the Sources list in section 9.
Legend: **P** = published figure (cited). **E** = estimate derived by this survey from published figures (the arithmetic is shown). **ROM** = unsourced rough order of magnitude. A ROM is *not* evidence, and a quote replaces it. "not published" = nothing found on the vendor's own pages.

---

## 1. Summary

**Headline:** None of the US candidates publishes a price for a 6-layer, double-sided SMT prototype. Every US finalist quotes only after you upload files, and most also need an account. A landed cost for the US options therefore **cannot be computed from published data**. The ranked list below uses capability fit, published fee rules, and the facts that decide landed cost: no setup, NRE, or stencil fees, consignment fees, and tax behavior.

| Rank | Finalist | US fab / assembly | Why | Landed cost, 5 boards, SMD only |
|---|---|---|---|---|
| 1 | **AdvancedPCB** (formerly Advanced Circuits/4pcb) | Fab: six US plants. Assembly: Aurora CO [S1][S3] | Publishes "no setup fees or NRE's for assembly" and says pricing "includes tooling, solder stencil" [S3]. No minimum quantity [S3]. Places LGA and 0201 parts [S2]. Consigned-part rules are simple [S2] | Quote required. ROM: $1.5k–4k excluding parts |
| 2 | **Summit Interconnect** (absorbed Advanced Assembly and Royal Circuits) | Assembly: Aurora/Denver CO. Fab: CA, IL, CO, **plus Toronto**, so you must request a US plant [S20][S21][S22] | Quick-turn prototype assembly at 3–4 day turns [S21]. Places 01005/0201 and BGA [S21] | Quote required; the Luminovo portal needs an account and an upload [S22]. ROM: $1.5k–4k excluding parts |
| 3 | **Sierra Circuits / ProtoExpress** | Fab and assembly: Sunnyvale / San Jose CA [S5][S7] | Online spec allows 4 mil trace/space and 6 mil holes [S6]. Online controlled impedance up to 6 layers at ±10% [S6]. Publishes a **$7 per consigned line** fee [S8] | Quote required; login and upload needed [S9][S10]. ROM: $1.5k–4k excluding parts |
| 4 | **Screaming Circuits + ASC Sunstone** | Assembly: Canby OR. Fab: Sunstone, Mulino OR [S11][S15] | Publishes a full attrition table, and a part costing ≥$5 (the SoM) needs **no** extra quantity [S12]. Minimum order is 1 [S11] | Quote required through the portal [S11]. ROM: $1.5k–4k excluding parts |
| Ref. | **JLCPCB** (China, not a candidate) | Fab and assembly: China | Standard PCBA is required because parts sit on both sides [S40] | **E ≈ $246 in published PCBA service fees**, then +35% US tariff (≈ $332), plus the bare PCB and parts (quote tool only), shipping (price not published), and OK tax, which JLCPCB collects [S41][S43][S45]. Details are in section 3 |

**Turnkey vs consigned (all finalists):** every finalist offers full turnkey, partial turnkey, and full consignment [S2][S5][S11][S21]. For LinHT the realistic model is **partial turnkey**: the fab buys the 76 other lines and you consign the MCM-iMX93 SoM. Published costs of consigning: Sierra charges $7 per consigned line [S8]. Screaming requires no extra SoM quantity because it costs ≥$5 [S12]. AdvancedPCB publishes no consignment fee [S2][S3]. Summit asks for "adequate overages" and gives no numbers [S21].

**Spec items no US candidate clearly meets from published data:**
- **0.1 mm (3.94 mil) clearance.** The published floors are 4 mil (Sierra online, Sunstone online, AdvancedPCB blog) or 4.5–5.5 mil (AdvancedPCB standard table). Every one of these is at or above 3.94 mil, so each fab needs a custom-spec review or a relaxed rule [S4][S6][S16].
- **1.0 mm thickness.** It is not a listed online option at Sierra (0.031"/0.062" listed [S6]) or Twisted Traces [S34]. It is inside the published range everywhere else, but only as custom spec.
- **0.2 mm drill vias.** Sunstone's online minimum drill is 0.008" (0.203 mm) and 0.2 mm is 0.00787", so this is marginal [S16].

---

## 2. Board spec (applied to every fab)

| Item | Value |
|---|---|
| Stackup | 6-layer FR4. 1.0 mm ±10%. Outer copper 0.5 oz, inner 1 oz. ENIG |
| Vias | Through-hole only. 668 × 0.3/0.6 mm and 5 × 0.2/0.5 mm (drill/pad, counted in `linht-hw.kicad_pcb`). No blind, buried, micro, or via-in-pad vias. No castellations |
| Rules | 0.15 mm (6 mil) track, 0.1 mm (≈3.9 mil) clearance. RF and USB nets are impedance-relevant |
| Size | 45.5 × 96 mm single board. kikit panel ≈ 67.5 × 118 mm |
| SMT | Both sides. 202 SMD footprints with `attr smd` (146 top, 56 bottom) and 868 SMD pads (counted from the PCB). 77 unique BOM lines. 0.4 mm QFN (BQ25792 QFN-29, ATtiny826 VQFN-20), several 0.5 mm QFNs, 168-pad 0.8 mm LGA SoM (consigned). Mostly 0402 passives |
| Not placed by the fab | J2, J5, SMA, audio jacks, encoder, THT LED, and wire pads are hand-fitted by the customer |
| Files | RS-274X Gerbers and Excellon (kikit). JLC-format BOM CSV (Comment, Designator, Footprint, LCSC, PN) with **no Manufacturer column**. CPL CSV. KiCad 10 project |

---

## 3. Comparison table

Y = published as supported. N = published as not supported. C = custom or offline quote. "—" = not published.

| Fab | US fab | US assy | 6L | 1.0 mm | ENIG | 6/4 mil | 0.3 mm / 0.2 mm drill | 0.4 mm pitch | 2-sided SMT | Turnkey / Partial / Consign | Min qty | Price basis | Lead time |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| AdvancedPCB [S1–S4] | Y (6 US plants) | Y (Aurora CO) | Y (Standard Spec up to 10L [S4b]) | C (not listed; 10% tolerance std) | — on caps page; ENIG multilayer expedite noted [S3] | C (4.5–5.5 mil std table; "premium" below 7 mil [S4]) | Y (vias need pad ≥ drill+10 mil; both via sizes meet it) | "fine pitch to .04 mils" (published typo) [S2] | Y [S2] | Y/Y/Y [S2] | none [S3] | Quote. No setup, NRE, or stencil charge [S3] | Multilayer std 5 days fab [S3]; assembly 3/5/10-day [S2] |
| Summit Interconnect [S20–S22] | Y, but specify US (Toronto plant exists) | Y (Aurora CO) | Y (≤10L instant) | — | Y [S22] | — | — | "fine pitch to .04 mils" (typo) [S21] | Y (BGA/µBGA) [S21] | Y/Y/Y [S21] | single prototype [S21] | Luminovo portal (account + upload) [S22] | 3–4 day turnkey assembly [S21]; fab 2–5 days [S22] |
| Sierra Circuits [S5–S10] | Y (Sunnyvale) | Y (Sunnyvale) | Y (online ≤12L) | C (online lists 0.031"/0.062"; range .005–.250") [S6][S7] | Y [S6] | Y online 4/4 [S6] | Y (6 mil min hole [S6]) | Y ("up to .35mm pitch") [S5] | — (implied) | Y/Y/Y [S5] | 1 [S10] | Portal (login + upload) [S9] | Assembly "as fast as 5 days" [S5]; +≥4 days over fab [S10] |
| Screaming Circuits + Sunstone [S11–S17] | Y (Mulino OR) | Y (Canby OR) | Y (Sunstone 1–20L instant [S15]) | C (0.020–0.125" listed; 1.0 mm not listed) [S16] | Y [S16] | Y online 4/4 [S16] (PCBExpress tier 5/5 fails [S17]) | 0.3 Y; 0.2 marginal (0.008" online min) [S16] | Y (0.35 mm) [S11] | — (not stated) | Y/Y/Y [S11] | 1 [S11] | Portal / Upload & Go [S14] | Sunstone fab from 24 h [S13] |
| MacroFab [S23–S26] | — (bare-board origin not stated; "North America") | Houston TX + network incl. Mexico [S23][S24] | Y | C (custom 0.008–0.248") | Y (std) | Y (3 mil) | Y (4 mil) | Y (0.3 mm leadless) [S24] | Y [S24] | Y/Y/Y | none | Upload quote | US-made only in 10-day service, **which excludes consignment** (2017 post) [S26] |
| CircuitHub / Worthington [S27–S31] | **Default Chinese fab**; domestic fab optional [S30] | Y (South Deerfield MA) [S28] | Y (2–10L std) [S29] | Y (1.0 mm listed) [S29] | Y (default) [S29b] | — | — | — | — | Turnkey + consign [S27] | — | Native-EDA upload quote [S27] | 3-day turnkey default [S27] |
| Bay Area Circuits [S18][S19] | Y (Fremont), offshore option exists [S19] | **via EMS partners** [S19] | Y | — | Y | — | 0.006" holes | — | — | Y/Y/Y [S18] | none [S18] | InstantDFM quote | Assembly from 3 days [S19] |
| PCB Unlimited [S32] | USA quickturn option (also Taiwan/China) | Y (Tualatin OR) | Y (2–8L USA) | Y (0.040") | Y | **N (5 mil min)** | — | Y (0.2 mm stated) | Y | Y/Y/Y | none | Instant quote (not submitted) | USA quickturn 24–48 h fab |
| Twisted Traces [S33][S34] | Claimed US (Elk Grove Village IL) | Claimed | 6L "quote request" | **N (not in calculator)** | Y | Calculator 5/5 or 6/6 only | 10/12 mil in calculator | — | — | Assembly offered | none | Upload + login | 4–5 working days |
| **JLCPCB (ref.)** [S40–S45] | China | China | Y | Y | Y (ENIG 2u, "$0") | Y (3.5 mil) | Y (0.15 mm min) | Standard 0.35 mm | **Standard only** (Economic is single-sided) [S40] | Y (consign needs JLC part # and China import) [S44] | 2 | Published fee table [S41] | Standard build ≥4 days; DHL 3–5 BD to N. America [S45] |

**JLCPCB reference build (E, from the published fee table [S41] and capabilities [S40]):**

| Line | Basis | USD |
|---|---|---|
| Setup, Standard, double-side | P | 51.12 |
| Stencil, double-side | P | 16.42 |
| Fixture, Standard rigid, 1–29 pcs (2 fixtures) | P | 16.42 |
| Feeder loading, 77 lines × $1.53 | E | 117.81 |
| SMT joints, 868 × 5 × $0.0016 | E | 6.94 |
| X-ray, 9 leadless parts × 5 = 45 pcs × $0.82 | E | 36.90 |
| Packing | P formula | ≈0.51 |
| **PCBA services subtotal** | E | **≈246** |
| US tariff pre-collected under DDP: PCB 35%, SMT 35% [S43] | E | ≈ +86 on services |
| Bare 6L PCB, 1.0 mm ENIG | "5pcs 6-layer … starts from $2" [S42]; price for this spec **not published** (quote tool only) | — |
| Components (76 lines turnkey) | quote tool only | — |
| Shipping DHL/FedEx to US | transit times published, **price not published** [S45] | — |
| OK sales tax | JLCPCB collects combined state and local tax at checkout [S46] | ≥4.5% |

JLCPCB caveats: Standard PCBA needs a single board or panel of at least **70 × 70 mm**. The 45.5 × 96 single board fails, and so does the 67.5 × 118 kikit panel (67.5 < 70) [S40]. Economic PCBA is single-sided and offers ENIG only at 1.6 mm [S40]. Consigning the SoM means shipping it to Zhuhai with a customs service fee of about $45 [S44].

---

## 4. Per-fab notes

**AdvancedPCB (formerly Advanced Circuits / 4pcb).**
- History: APCT merged with Advanced Circuits in February 2023, and in June 2024 APCT, Advanced Circuits, and San Diego PCB Design combined as AdvancedPCB [S1b]. 4pcb.com now 301-redirects to advancedpcb.com [S1].
- Plants: Aurora CO (HQ, 21101 E. 32nd Pkwy), Santa Clara CA, Chandler AZ, Orange CA, Maple Grove MN, Placentia CA. "All of our printed circuit boards are manufactured in USA facilities" [S1c][S4].
- Files: fab needs Gerber RS-274X plus Excellon and a tool list; ODB++ and DXF are also accepted [S3]. Assembly needs a BOM and CPL; "CAD and ODB data accepted" [S2]. KiCad native: not published.
- Consigned parts: package and label each part with its BOM line. Parts not on reel need continuous tape with a leader of at least 6", and an inventory list with MPN and quantity. Unused parts are returned [S2][S3]. Attrition percentage: not published.
- Pricing: no setup, NRE, or stencil charges [S3]. The only published specials are 2L at $33 and 4L at $66 [S1d]. 6-layer price: not published.
- Shipping: UPS, FedEx, DHL [S3]. Sales tax behavior: not published.

**Summit Interconnect.**
- Acquired Royal Circuit Solutions (Hollister CA) and Advanced Assembly (Aurora CO) in 2022 [S20]. Advanced Assembly rebranded as Summit on 2025-01-07, and the legal entity is still Advanced Assembly, LLC [S20b].
- Quick-turn assembly at 20100 E. 32nd Pkwy, Aurora CO [S21].
- Consignment: "properly labeled and packaged" with "adequate overages" [S21]. Attrition percentage: not published.
- Instant portal handles boards up to 10 layers; account and upload required [S22]. Plants include Toronto, so **specify US fabrication** on the order.
- BOM columns: not published. Sales tax: not published.

**Sierra Circuits.**
- Assembly at 1108 W. Evelyn Ave, Sunnyvale. Consigned parts go to 1980 Lundy Ave, San Jose [S5][S7].
- Online ordering: 1–1,500 boards, up to 12 layers, 4/4 mil, 6 mil hole [S6][S10]. Controlled impedance online: ≤6 layers, ±10% only, ≤4 layers, ≤2 impedances per layer [S6]. Impedance cost: not published.
- Files: Gerber, ODB++, or IPC-2581; BOM in .xlsx; XY data; assembly drawing [S7]. A KiCad quote plugin exists [S5]. The FAQ asks for "correct part number, description, and component values"; a Manufacturer column is not explicitly required [S7].
- Consignment: quantities come from a CCI form (shortage plus attrition), and unused attrition is scrapped (returning it costs $300). Each consigned line costs $7. Parts on continuous tape, no splices [S8]. Sierra prefers you consign only hard-to-find or custom parts, which covers the SoM [S8].
- Duties and tariffs are the customer's responsibility. Ships FedEx/UPS [S10]. Sales tax: not published.

**Screaming Circuits (Milwaukee Electronics) + ASC Sunstone.**
- Assembly at 1140 NW 3rd Ave, Canby OR. Screaming does not fabricate; it orders boards from ASC Sunstone [S11]. Sunstone is at 13626 S. Freeman Rd, Mulino OR [S15].
- Files: minimum set is a BOM (.xls or .xlsx), Gerbers, and a centroid file [S11]. The BOM guide stresses MPNs, refdes, quantities, and mounting type [S13b]. Manufacturer column: not stated. KiCad native: not published.
- Attrition [S12]: 0201/0402 parts need +20% with a minimum of 50 extra. 0603–1206 parts need +10% with a minimum of 20. THT parts need +2. Other parts are tiered by unit cost, and parts costing ≥$5 need the exact quantity only.
- Screaming orders its own stencil even when you supply one [S11]. It prefers a panel when any board dimension is under 55 mm. LinHT is 45.5 mm wide, so **send the kikit panel**. Panel limits: 3"×3" minimum, 14"×19" maximum [S13].
- Sunstone online (instant) tier: 4/4 mil, 0.008" drill, ENIG, impedance "Yes" [S16]. The PCBExpress quickturn tier is 5/5 mil with a 0.010" hole, which **fails** [S17].
- Ships UPS by default [S11]. Sales tax and pricing: not published.

**MacroFab.**
- Houston TX HQ and prototyping facility, plus a network in the USA, Mexico, and Canada [S23][S24].
- A 2017 post says 10-day orders are turnkey only: ≤50 units, <20 unique SMT lines, **no consignment** [S26]. LinHT has 77 lines and a consigned SoM, so it does not qualify. The origin of non-10-day builds is not guaranteed to be the US. A 2024 post claims "US-built, ITAR-compliant bare PCBs" [S25].
- Help-center pages (overage, required files) did not render: not published in readable form.
- Treat as **conditional**: ask in writing for US-only fab and assembly.

**CircuitHub (built by Worthington Assembly).**
- Worthington is "the exclusive manufacturing partner for CircuitHub" at South Deerfield MA [S28].
- Needs native EDA upload, and "Compatible with … KiCAD" [S27]. Standard thicknesses include 1.0 mm [S29].
- Bare boards come by default from a Chinese fabricator. A domestic-fab option exists, and its "price may be slightly higher" [S30].
- Treat as **conditional**: choose domestic fab.
- Worthington's own consignment rules: 0201/0402 parts +50% with a minimum of 50 extra. Every package must be marked with the MPN. Multiple cut-tape pieces of one part are not accepted [S31].

**Bay Area Circuits.** Fab is in Fremont CA, and an offshore fab option exists [S19]. Assembly is "delivered through an integrated process with trusted EMS partners" [S19], so the assembler's location is not published. Kitting rules: 0402 parts +20% with a minimum of 20. Continuous cut tape of at least 6" [S18].

**PCB Unlimited.** Assembly in Tualatin OR. The USA quickturn option is 2–8 layers with 0.040" thickness available, but its 5 mil minimum trace/space **fails** the spec [S32]. The BOM must include MPNs [S32].

**Twisted Traces.** Elk Grove Village IL, and claims "on-shore PCBs" [S33]. The public calculator lists 6L as "quote request", thicknesses 0.031/0.062/0.093/0.125" only, 5/5 or 6/6 mil, and 10/12 mil holes [S34]. **Fails** 1.0 mm and 4 mil as published. Whether it owns its plant is not published.

---

## 5. Excluded / not US-made / defunct

| Company | Reason |
|---|---|
| OSH Park | Bare boards only. The 6L service is 1.6 mm only, with a 5 mil minimum. It is "Manufactured in the United States" but offers no assembly [S35] |
| Tempo Automation | Cut 62 of 69 staff in July 2023 [S36]. Delisted from Nasdaq in November 2023 [S37]. Chapter 7 filing reported December 2023 (secondary source only; court or SEC record not retrieved) |
| Royal Circuits | Acquired by Summit Interconnect in 2022. royalcircuits.com refused connections on the access date [S20] |
| Advanced Assembly | Now Summit Interconnect Denver. aapcb.com refused connections [S20b] |
| San Diego PCB | Merged into AdvancedPCB in 2024 as a design unit [S1b] |
| Saturn Electronics | Bare-board fab only (Romulus MI), with offshore options [S38] |
| Worthington Assembly (standalone) | Assembly only; you must supply the boards [S39]. Usable only when paired with a US fab |
| JLCPCB | Chinese fab and assembly; reference row only |

---

## 6. File-prep gaps for finalists

| Gap | AdvancedPCB | Summit | Sierra | Screaming/Sunstone |
|---|---|---|---|---|
| Add a **Manufacturer** column and a Qty column; rename PN→MPN; drop the LCSC column or keep it as info | Yes (the consignment list needs MPN [S3]) | Yes | Yes (.xlsx BOM [S7]) | Yes (use their sample .xlsx [S13b]) |
| BOM as .xlsx, not CSV | — | — | Required [S7] | .xls/.xlsx [S11] |
| Panel vs single board | Not published; ask | Not published | Not published | **Send the kikit panel** (board <55 mm [S13]) |
| Fab notes: 1.0 mm ±10%, ENIG, 0.5/1 oz, 6/4 mil, 0.2 mm vias, impedance nets | Custom spec needed for <4.5 mil space | Specify a **US plant** | 1.0 mm is not an online option: custom | Use the online instant tier (4/4, 0.008"). Flag the 0.2 mm drill |
| Consigned SoM | Label it with its BOM line; tray or original packaging | Label it and include "adequate overage" | CCI form, $7 per line. SoM is exactly the kind of part they accept consigned | Exact quantity (≥$5 part) [S12] |
| Mark DNP/hand-fit parts (J2, J5, SMA, jacks, encoder, LED) in BOM and CPL | Yes | Yes | Yes | Yes |
| CPL: add units and side columns in their format; confirm rotation convention | Yes | Yes | "X-Y data" [S7] | Centroid [S11] |
| Assembly drawing (top and bottom) | — | — | Required [S7] | — |

---

## 7. J5 backup part

**Repo footprint** (`parts/parts.pretty/Connector_FFC_01x20_P0.75mm.kicad_mod`, read directly):
- 20 SMD roundrect pads, each 2.0 × 0.5 mm, on a 0.75 mm pitch. They form one column from y = 0 to −14.25 mm at x = 0.
- **No mounting or solder-tab pads.**
- Silk and body outline runs from x = −0.8 to +3.9 mm and y = −16.1 to +1.9 mm, so the body sits on +x, about 4.7 × 18 mm.
- Description: "Display connector with 0.75 mm pitch and 0.5 mm pads".
- The schematic has J5 = "LCD" with empty LCSC and Mouser fields (`display.kicad_sch`).
- Contact side (top/bottom) is not encoded in the footprint.

**Result: no matching distributor part was found.** The Mouser and Digi-Key parametric filters for 0.75 mm pitch could not be read: Mouser timed out, and Digi-Key sits behind a bot-verification page that was not bypassed. Web searches of the Mouser, Digi-Key, LCSC, Molex, Hirose, TE, and Amphenol listings returned only 0.5 mm and 1.0 mm pitch parts. A catalog ZIF/LIF FPC connector would also need solder-tab pads that this footprint does not have. So **no distributor part can be claimed to match**. Next steps:
1. Run Digi-Key's filter yourself (FFC/FPC connectors, pitch 0.030" / 0.75 mm, 20 positions, SMT).
2. Measure the C62 donor connector.
3. Consider redesigning J5 to a standard 0.5 mm part together with a new display FPC.

---

## 8. Oklahoma tax note

**Rates and use tax**
- The state sales tax is **4.5%** of gross receipts from tangible personal property [S47].
- Use tax is due on tangible personal property "purchased and brought into this state for storage, use or consumption" [S47]. Local city and county use tax is added and **varies by address**; use the OTC rate locator [S47].

**Custom-made boards**
- Articles fabricated "according to the special order of their customers" are taxable on total receipts, and the seller cannot deduct labor [S48] (OAC 710:65-19-60). A turnkey PCBA is therefore taxable.
- Labor-only assembly on customer-consigned parts: **no specific OTC rule found** (not published). Treat it as taxable unless the OTC says otherwise.

**Who pays**
- Remote sellers with ≥$100,000 of Oklahoma sales must collect the tax. If a seller does not collect, the purchaser reports use tax on the Consumer Use Tax Return, through OkTAP, or on Form 511 [S49][S50].
- Separately stated delivery charges are not taxable; delivery included in the price is taxable [S48b] (OAC 710:65-19-70).
- JLCPCB collects combined state and local sales tax at checkout [S46].

---

## 9. Sources (all accessed 2026-09-24)

- S1 https://www.advancedpcb.com/en-us/ (4pcb.com 301-redirect target)
- S1b https://www.advancedpcb.com/en-us/now-advanced-pcb/
- S1c https://www.advancedpcb.com/en-us/company/about/
- S1d https://www.advancedpcb.com/en-us/resources/pricing/
- S2 https://www.advancedpcb.com/en-us/solutions/assembly-services/
- S3 https://www.advancedpcb.com/en-us/company/faqs/
- S4 https://www.advancedpcb.com/en-us/resources/manufacturing-capabilities/
- S4b https://www.advancedpcb.com/en-us/resources/blog/standard-vs-custom-spec-printed-circuit-boards-advanced-circuits/
- S5 https://www.protoexpress.com/pcb-assembly/
- S6 https://www.protoexpress.com/kb/web-pcb-specs/
- S7 https://www.protoexpress.com/faq/pcb-assembly/ ; https://www.protoexpress.com/kb/rigid-pcb/
- S8 https://www.protoexpress.com/kb/kitting-guidelines/
- S9 https://www.protoexpress.com/products/sierra-standard-product/
- S10 https://www.protoexpress.com/products/online-pcb-manufacturing/
- S11 https://www.screamingcircuits.com/faq
- S12 https://www.screamingcircuits.com/guides/attrition-standards-and-conditions
- S13 https://www.screamingcircuits.com/guides/pcb-panel-guidelines ; https://www.screamingcircuits.com/services/pcb-fabrication
- S13b https://www.screamingcircuits.com/guides/bom-upload-guide-faster-pcb-assembly-quote
- S14 https://portal.screamingcircuits.com/upload-and-go
- S15 https://www.sunstone.com/about-sunstone/where-we-are-located ; https://www.sunstone.com/pcb-manufacturing-capabilities
- S16 https://www.sunstone.com/pcb-manufacturing-capabilities/detailed-capabilities
- S17 https://www.sunstone.com/pcb-products/pcb-manufacturing/pcbexpress-quickturn
- S18 https://bayareacircuits.com/kitting/ ; https://bayareacircuits.com/quick-turn-and-full-turn-key-pcb-assembly-services/
- S19 https://bayareacircuits.com/our-services/ ; https://bayareacircuits.com/pcb-circuit-board-fabrication/
- S20 https://summitinterconnect.com/blog/article/royal-circuits-acquired-by-summit/ ; https://summitinterconnect.com/
- S20b https://summitinterconnect.com/blog/article/advanced-assembly-announces-name-change-to-summit-interconnect/
- S21 https://summitinterconnect.com/turnkey-pcb-assembly/ ; https://summitinterconnect.com/pcb_assembly/
- S22 https://summitinterconnect.com/quick-turn-pcb-services/
- S23 https://www.macrofab.com/pcb-assembly/
- S24 https://www.macrofab.com/capabilities
- S25 https://www.macrofab.com/blog/bare-pcb-launch
- S26 https://www.macrofab.com/blog/macrofab-now-offers-10-day-prototyping/
- S27 https://www.circuithub.com/
- S28 https://www.worthingtonassembly.com/circuithub-1
- S29 https://www.circuithub.com/capabilities/pcb-stackups (thickness list via site search result) ; S29b https://www.circuithub.com/capabilities/design-rules
- S30 https://www.circuithub.com/post/mitigating-long-lead-times-during-the-2024-chinese-new-year-for-your-pcb-assembly-needs
- S31 https://www.worthingtonassembly.com/consigned-material
- S32 https://www.pcbunlimited.com/products/usa-pcb-assembly ; https://www.pcbunlimited.com/
- S33 https://www.twistedtraces.com/faq ; https://www.twistedtraces.com/about-us
- S34 https://www.twistedtraces.com/online-quote
- S35 https://docs.oshpark.com/services/six-layer/
- S36 https://www.sec.gov/Archives/edgar/data/1813658/000110465923081448/tm2321430d1_8k.htm
- S37 https://www.globenewswire.com/news-release/2023/10/27/2768445/0/en/Tempo-Automation-Holdings-Inc-Announces-Commencement-of-Nasdaq-Delisting-Proceedings.html
- S38 https://www.saturnelectronics.com/
- S39 https://www.worthingtonassembly.com/ ; https://www.worthingtonassembly.com/request-a-quote
- S40 https://jlcpcb.com/capabilities/pcb-assembly-capabilities
- S41 https://jlcpcb.com/help/article/pcb-assembly-price
- S42 https://jlcpcb.com/6-layer-pcb ; https://jlcpcb.com/help/article/in-what-cases-will-there-be-charged-extra
- S43 https://jlcpcb.com/help/article/us-tariff-policy-faq (rate table image https://rs.jlcpcb.com/static/image/news/Tariff-us.png)
- S44 https://jlcpcb.com/help/article/important-note-before-you-consign-the-part-to-jlcpcb
- S45 https://jlcpcb.com/help/article/shipping-methods-and-delivery-time
- S46 https://jlcpcb.com/help/article/about-us-state-sales-and-use-taxes (via site search result)
- S47 https://oklahoma.gov/tax/businesses/sales-use-tax.html
- S48 https://oklahoma.gov/content/dam/ok/en/tax/documents/resources/rules-and-policies/agency-rules/Chapter65-2022.pdf (OAC 710:65-19-60) ; S48b same document, OAC 710:65-19-70
- S49 https://oklahoma.gov/content/dam/ok/en/tax/documents/resources/publications/streamlines-sales-tax/WayfairFAQs-06152020.pdf
- S50 https://oklahoma.gov/content/dam/ok/en/tax/documents/resources/publications/infographics/SalesTaxUseTax.pdf
