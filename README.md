# CMOS C/R Visualizer

A browser-only tool for visualizing parasitic capacitance and resistance networks from CMOS extraction-style netlists.

## Features

- Paste or upload extraction text.
- Parse SPICE-like `C`, `R`, and MOS instance lines.
- Visualize capacitance by net and by element.
- Summarize capacitance hanging from each node, split into grounded and coupling contribution.
- Visualize a focused R ladder around a selected node instead of drawing every resistor in a large netlist.
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

For SPICE-like rows, bare resistance values on `R` lines are treated as ohms. Bare capacitance values on `C` lines use the `Bare C unit` selector in the UI, with fF as the default. Select `F` when you want strict SPICE-style unitless capacitance values.

PEX-style MOS rows with model names and parameters are accepted:

```spice
MMP0 OUT_M1 IN_M1 VDD_M1 VDD_M1 pmos_lvt W=1.0u L=40n
MMN0 OUT_M1 IN_M1 VSS_M1 VSS_M1 nmos_lvt W=0.5u L=40n
RIN_0001 IN IN_1 2.31
CIN_0001 IN VSS 0.21f
```

The parser ignores simulator control lines such as `.subckt`, `.model`, `.tran`, and source/load statements unless they begin with `R`, `C`, `M`, or `X` in a supported form.

## Use

Open `index.html` in a browser. No server or build step is required.

For large PEX decks:

1. Paste or upload the deck and click Analyze.
2. Open Capacitance and inspect Node Capacitance Summary.
3. Click a node name, or type it into R focus node.
4. Open R Ladder and adjust R depth to inspect only the local resistance ladder around that node.
