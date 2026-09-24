# LinHT Hardware

Hardware design for the LinHT handheld and the vocabulary for getting it built.

## Language

### Manufacturing

**Fab files**:
The manufacturing outputs a board house works from: Gerbers, BOM, and pick-and-place (CPL) files.
_Avoid_: CAD files (those are the KiCad sources)

**CAD files**:
The native KiCad project sources (schematics, PCB, libraries).

**Build scope**:
How much of the board a fab takes on: **bare PCB**, **partial turnkey**, **turnkey**, or **consigned**.

**Bare PCB**:
An unpopulated board: fabrication only, no assembly.

**Turnkey**:
The fab buys every BOM part and assembles the whole board.

**Partial turnkey**:
The fab sources and places some parts; the builder supplies or fits the rest.

**Consigned part**:
A part the builder buys and ships to the fab for it to place (e.g. the SoM).

**Hand-fit part**:
A part the builder solders after the fab returns the board, including donor parts.

**Donor parts**:
Parts reused from a Retevis C62 radio (SMA, audio jacks, encoder, display, enclosure).

**US fab**:
A board house that fabricates and assembles in the United States. A US company that fabricates offshore is not a US fab.

**Landed cost**:
Everything paid until boards arrive: quote, setup/NRE, stencil, shipping, tariffs and duties.
_Avoid_: price (ambiguous)

## Relationships

- A **Build scope** splits the BOM into fab-placed, **Consigned parts**, and **Hand-fit parts**
- **Donor parts** are always **Hand-fit parts**

## Flagged ambiguities

- "board build" could mean anything from a **Bare PCB** to **Turnkey**; resolved: compare fabs by the largest **Build scope** each offers, with the builder completing the rest.
