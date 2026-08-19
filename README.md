# AvionixForge

A browser-based visual designer for building custom RC aircraft instrument clusters, exporting each design as a ready-to-flash Arduino sketch that renders live MAVLink telemetry on a physical LCD/OLED/TFT panel.

No installation, no build step — it's a single self-contained HTML file. Open it in a browser and start designing.

## How it works

Start it with this link:
https://gonnir.github.io/Avionix-Forge/

The manual is available here:
https://gonnir.github.io/Avionix-Forge/manual.html

1. **Design in the browser.** Drag instruments (artificial horizon, airspeed tape, compass, gauges, decorative shapes, etc.) onto a live canvas sized to match your actual display. Position, resize, recolor, and rotate each one; the canvas is a pixel-accurate preview of what the real hardware will show, running on simulated demo data so you can see it move before anything is wired up.

2. **Configure your hardware once.** Pick your microcontroller (RP2040 tested so far, ESP32, ESP32-S3 coming soon), your display panel, its wiring pins, and your MAVLink UART settings in a single setup dialog.

3. **Export.** One click generates a complete, self-contained `.ino` sketch — display driver initialization, MAVLink parsing, and a dedicated draw function per instrument, all in plain Arduino/C++ using standard libraries (Adafruit GFX/U8g2). Nothing to hand-edit.

4. **Flash and fly.** Load the sketch in the Arduino IDE, upload it to your board, wire the board's UART to your flight controller's telemetry port, and the cluster comes alive with real flight data.

## What it generates

- A single `.ino` file with no external project dependencies beyond the display/MAVLink libraries already used by the Arduino ecosystem
- Board-appropriate performance handling (e.g. dual-core telemetry offload on RP2040, framebuffer/double-buffering when RAM allows)
- Every instrument's appearance (colors, sizing, text) baked in as generated code — the exported sketch has no runtime dependency on the design tool

## Supported instruments

Artificial horizon, airspeed/altitude/heading/groundspeed/VSI tapes and dials, compass, turn coordinator, arc and bar gauges, flight mode indicator, home distance/direction, custom text-value readouts, static labels, and decorative panel shapes (rectangles, circles, lines, screws) for building a cohesive panel layout.

## Requirements

- Any modern desktop browser to run the designer
- Arduino IDE (or CLI) to compile and flash the generated sketch
- A supported microcontroller + display combination
- A flight controller streaming MAVLink telemetry (ArduPilot or iNav) over a serial connection to the board

## Project files

Designs can be saved to and loaded from a plain JSON file, so a cluster layout is fully portable and version-controllable independent of the generated Arduino code.

## License

See `LICENSE` for details.
