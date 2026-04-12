# The Luxembourg Effect

An interactive simulator and companion paper exploring **ionospheric cross-modulation** — the phenomenon where a powerful radio transmitter modifies the ionosphere's absorptive properties, imprinting its audio onto unrelated signals passing through the same region.

First observed by B. D. H. Tellegen in Eindhoven on April 10, 1933, when listeners tuned to Beromünster (652 kHz, Switzerland) heard Radio Luxembourg's (230 kHz) program content faintly superimposed on the signal. The ionosphere was acting as a nonlinear mixer.

**[Launch the simulator](https://gregzancewicz.github.io/luxembourg-effect/)** · **[Read the paper (PDF)](https://github.com/GZancewicz/luxembourg-effect/blob/main/luxembourg_effect.pdf)**

---

## Interactive Simulator

A self-contained single-page application (`index.html`) that models the 1933 observation in real time. No build step, no dependencies — just open it in a browser.

### Features

- **Three real stations**: Radio Luxembourg (230 kHz, Junglinster), Beromünster (652 kHz, Switzerland), and a receiver at Eindhoven — with historically accurate default power levels (150 kW / 60 kW)
- **Live controls**: Adjust transmitter power, audio tone frequency, and modulation depth for both stations, plus ionospheric parameters (collision frequency, electron density)
- **Signal path map**: Shows the geographic layout with the ionospheric interaction region
- **Spectrum display**: Beromünster's carrier with its own AM sidebands (green) and the unwanted Luxembourg cross-modulation sidebands (blue), plotted in dB with levels that respond to parameter changes
- **Modulation transfer function**: Log-frequency plot showing the low-pass character of cross-modulation, with the −3 dB cutoff frequency marked
- **Audio synthesis**: Listen to the signal at Eindhoven via Web Audio API — hear both Beromünster's tone and the faint Luxembourg cross-modulation tone in real time
- **Info popups**: Click the (i) icon on any parameter or derived quantity for an explanation
- **Derived quantities**: E-field at ionosphere, relaxation time τ, heating ΔT, and −3 dB frequency, all updated live
- **Restore defaults**: One-click reset to the historical 1933 parameters

### Physics Model

The simulator implements the linearized cross-modulation theory:

1. **Friis equation** — computes Luxembourg's E-field at the ionosphere (~85 km altitude)
2. **Electron energy balance** — RF heating vs. collisional cooling determines ΔT
3. **Collision frequency modulation** — ν(Tₑ) ∝ √Tₑ links temperature to absorption
4. **Cross-modulation transfer integral** — mw = (2m / √(1 + Ω²τ²)) · ∫ β·κ₀·ΔT̄/T₀ ds

The model correctly reproduces the saturation behavior at high power and the low-pass frequency response (bass transferred more effectively than treble, consistent with the historical "muffled" quality of the cross-modulation).

## Companion Paper

`luxembourg_effect.tex` — a 14-page LaTeX paper covering:

1. **Historical background**: Tellegen's 1933 discovery, Bailey & Martyn's 1934 theoretical explanation, the Beromünster dead-air tests, van der Pol & van der Mark's systematic measurements, the Luxemburg–Gorky effect, and the line from the original observation to modern facilities like HAARP
2. **Full theoretical derivation from first principles**:
   - Maxwell's equations in a weakly ionized plasma
   - Electron equation of motion (Langevin/Drude model)
   - Complex dielectric function and refractive index
   - The Appleton–Hartree equation (origin, significance, and simplification for cross-modulation)
   - Absorption coefficient and its dependence on collision frequency
   - Electron energy balance (RF heating, collisional cooling, relaxation time)
   - Temperature dependence of collision frequency
   - Cross-modulation transfer integral — the central result
3. **Discussion**: validity of linearization, role of the geomagnetic field, altitude dependence, frequency dependence, connection to nonlinear optics

### Building the PDF

Requires a LaTeX distribution (e.g., TeX Live, MacTeX):

```bash
pdflatex luxembourg_effect.tex
pdflatex luxembourg_effect.tex   # second pass for cross-references
```

## Project Structure

```
index.html               Interactive simulator (single-file, no dependencies)
luxembourg_effect.tex    LaTeX source for the companion paper
luxembourg_effect.pdf    Compiled paper
LICENSE                  MIT License
```

## License

[MIT](LICENSE)
