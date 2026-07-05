Eine WebGL-Fluid-Simulation im Stil von iog.io — Navier-Stokes ("Stable Fluids" nach Jos Stam)
komplett auf der GPU, ohne Dependencies, in einer einzigen `index.html`.

## Starten

Einfach `index.html` im Browser öffnen (Doppelklick genügt), oder mit lokalem Server:

```
python -m http.server 4173
```

→ http://localhost:4173

## Steuerung

| Eingabe | Wirkung |
| --- | --- |
| Maus bewegen | Fluid stören (Farbspur) |
| Klick / Touch | Splash |
| Leertaste | Pause |
| B | Farb-Burst |
| "Fluid GPU"-Chip unten rechts | Einstellungs-Panel |

## Features

- **Simulation:** Semi-Lagrange-Advektion, Jacobi-Drucklöser (24 Iterationen),
  Vorticity Confinement für die charakteristischen Wirbel — Sim-Grid bis 256er
  Auflösung, Farbtextur bis 2048 (Preset "Ultra").
- **Rendering:** Volumetrische Lichtabschattung (Sunrays), Normal-Shading auf
  der Farbdichte; optional HDR-Bloom (Multi-Pass Downsample/Upsample,
  standardmäßig aus — im Panel zuschaltbar).
- **Tempo-Regler:** Globaler Zeitfaktor (Standard 0.3, entspannt-langsam)
  verlangsamt die ganze Simulation gleichmäßig — von Zeitlupe (0.2) bis
  doppelter Geschwindigkeit (2.0).
- **Harmonische Farbpalette:** Ein Basis-Farbton driftet langsam übers Farbrad;
  alle Farben (Maus, Emitter, Bursts) bleiben in seiner Nachbarschaft —
  wechselnde, aber immer stimmige Kombinationen.
- **Funken-Partikel:** 65.536 GPU-Partikel (RGBA32F-Ping-Pong), die vom
  Geschwindigkeitsfeld advektiert werden und nur in hellen, schnellen
  Bereichen aufleuchten (standardmäßig aus, im Panel zuschaltbar).
- **Auto-Flow:** Zwei unsichtbare Emitter auf gegenläufigen Lissajous-Bahnen —
  ein Haupt-Band mit heißem Komplementär-Kern und ein Gegen-Band mit
  versetztem Farbton — weben ohne Interaktion eine durchgehende Komposition
  (abschaltbar im Panel).
- **Fallbacks:** WebGL2 mit Half-Float bevorzugt; WebGL1-Fallback mit manueller
  bilinearer Filterung, reduzierten Effekten und ohne Partikel.

Architektur der Render-Pipeline inspiriert von Pavel Dobryakovs
[WebGL-Fluid-Simulation](https://github.com/PavelDoGreat/WebGL-Fluid-Simulation) (MIT).
