# CMOS C/R Visualizer

A browser-only tool for visualizing parasitic capacitance and resistance networks from CMOS extraction-style netlists.

## Features

- Paste or upload extraction text.
- Parse SPICE-like `C`, `R`, and MOS instance lines.
- Visualize capacitance by net and by element.
- Visualize an RC net graph where nodes are nets and edges are resistance elements.
- Show MOS device mappings for lines such as:

```spice
XPU1 PN A VDD pmos
XPU2 PN B Y pmos
XPD1 Y A VSS nmos
XPD2 Y B VSS nmos
```

## Input Examples

```spice
XPU1 PN A VDD pmos
XPU2 PN B Y pmos
XPD1 Y A VSS nmos
XPD2 Y B VSS nmos
R_XPU1_CH VDD PN 46.0
R_XPU2_CH PN Y 49.5
C_Y_METAL Y VSS 15.2f
C_PN_TO_Y PN Y 1.5f
```

Node names with extraction point suffixes are also accepted:

```spice
XPU1 PN:300 A VDD pmos
XPU2 PN:301 B Y pmos
XPD1 Y A VSS nmos
XPD2 Y B VSS nmos
C PN:300 PN:301 100
R PN:300 VSS 1000
```

For SPICE-like rows, bare capacitance values on `C` lines are treated as fF. Bare resistance values on `R` lines are treated as ohms.

## Use

Open `index.html` in a browser. No server or build step is required.
