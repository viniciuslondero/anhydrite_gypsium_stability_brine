# Gypsum–Anhydrite Stability in NaCl Brine

An interactive, single-page tool that shows where calcium sulfate is stable as **gypsum** (CaSO₄·2H₂O) or **anhydrite** (CaSO₄) as NaCl concentration, pressure and temperature change.

Each surface is a *transition temperature* T<sub>t</sub>(m, P): above it anhydrite is stable, below it gypsum.

## Usage

Open `index.html` in a browser. It is self-contained: the PHREEQC grid and the P–T path are embedded in the page. An internet connection is needed only to load Plotly (from cdnjs) and the web fonts.

The page has:

- **Controls:** sliders for NaCl concentration (mol/kg), pressure (MPa) and temperature (°C), plus example conditions (seawater at the start of leaching, a half-saturated brine, a saturated deep cavern, a shallow flooded salt mine, and others).
- **Readout:** the stable phase, transition temperature and margin (T − T<sub>t</sub>) under each model, and the gap between the two models.
- **P–T path over time:** a 3,200-day series at 5.7 mol/kg NaCl (from `PT_Tempo.csv`; pressure converted from bar to MPa). Drag the day slider or press Play to move along the path.
- **Editable series:** under "Edit the series", change any cell (day, pressure, temperature, NaCl), add or delete rows, import a CSV file, paste rows copied from a spreadsheet, download the current series as CSV, or reset to the original. Pressure can be shown and entered in bar or MPa. Imports take columns in the order day, pressure, temperature, NaCl (NaCl optional), or match them by a header row. Edits are saved in your browser's local storage and stay only on that browser.
- **3D stability surfaces:** both models, with the measured transitions at 0.1 MPa and the selected point.
- **2D section** at the selected pressure, showing where the models agree on gypsum, agree on anhydrite, or disagree.
- **Method notes and sources.**

## Models

### 1. Measured data + pressure slope

```
T_t = 56 − 3m − 0.5m² + (P − 0.1) / 7.8      (°C; m in mol/kg; P in MPa)
```

- **NaCl effect at 0.1 MPa:** transitions of 56, 52, 48, 36 and 20 °C at 0, 1, 2, 4 and 6 mol/kg (Blount & Dickson 1973, tabulated by Berdugo et al. 2008). The quadratic fits all five within 0.5 °C.
- **Pressure effect:** +1 °C per 7.8 MPa (Blount & Dickson, as adopted by Berdugo et al.). It was measured in pure water and is applied unchanged at every salinity.

### 2. PHREEQC Pitzer

- PHREEQC 3 (via `phreeqpython`) with the `pitzer.dat` database. For each NaCl concentration and pressure, the brine is equilibrated with anhydrite, and the temperature where gypsum's saturation index reaches zero is found by bisection.
- Computed on a 26 × 11 grid (0–6.2 mol/kg, 0.1–100 MPa) and interpolated between nodes.

### How they compare

Both give 56 °C in pure water and about +12 to +13 °C per 100 MPa. They diverge with salinity: at 6 mol/kg PHREEQC gives about 34 °C, against about 20 °C measured. Zen (1965) and Hardie (1967) also place the transition below 20 °C near halite saturation, so the measured model is likely closer at high salinity. The PHREEQC gap probably reflects Ca–SO₄ Pitzer parameters fitted mainly to seawater-type brines; this attribution is an interpretation and is not tested here.

## Limitations

- Pressure acts on both the fluid and the solids. If the rock carries a higher load than the pore fluid, the behavior differs (MacDonald 1953).
- Both are equilibrium models. Below about 100 °C anhydrite reacts very slowly, so either phase can persist metastably near the boundary.
- Halite saturation is taken as 6.15 mol/kg (25 °C); values above 6 mol/kg are a short extrapolation.
- The example conditions are illustrative.

## Sources

- Blount, C. W. & Dickson, F. W. (1973). Gypsum–anhydrite equilibria in systems CaSO₄–H₂O and CaSO₄–NaCl–H₂O. *American Mineralogist* 58, 323–331. <https://msaweb.org/AmMin/AM58/AM58_323.pdf>
- Berdugo et al. (2008). <https://raccefyn.co/index.php/raccefyn/article/download/2340/3741>
- Hardie, L. A. (1967). The gypsum–anhydrite equilibrium at one atmosphere pressure. *American Mineralogist* 52, 171–200. <https://msaweb.org/AmMin/AM52/AM52_171.pdf>
- MacDonald, G. J. F. (1953). Anhydrite–gypsum equilibrium relations. *American Journal of Science*. <https://ajsonline.org/article/58427>
- Monnin, C. (1990). <https://www.osti.gov/biblio/6054036>
- PHREEQC version 3 (USGS). <https://www.usgs.gov/software/phreeqc-version-3>
