<img width="499" height="344" alt="Screenshot 2026-08-03 171317" src="https://github.com/user-attachments/assets/4a281c9f-f4d2-4539-9451-8743e6cfecda" />
# ERGOmouse
# ErgoMouse
 

# README.md

```markdown


Generate a custom, 3D-printable ergonomic mouse shell from a few photos of your hand.

## What it does

HandFit Mouse takes photos of your hand, extracts hand measurements (palm width,
finger lengths, thumb position) using landmark detection, and generates a
parametric 3D model of a mouse shell shaped to fit your hand. The model can be
exported as an STL, 3D printed, and assembled with standard mouse electronics
(optical sensor, switches, scroll wheel) into a fully functional mouse.

## How it works

1. **Capture** — Take two guided photos of your hand: a top-down palm shot with
   fingers spread, and a side-profile shot with a credit card in frame for scale.
2. **Landmark detection** — MediaPipe Hands extracts 21 hand landmarks per photo.
3. **Measurement extraction** — Palm width, per-finger lengths, and thumb
   CMC angle/offset are calculated from the landmarks, scaled to millimeters
   using the credit card as a size reference.
4. **Parametric modeling** — Measurements are mapped onto a parametric mouse
   shell built in CadQuery, adjusting the palm cradle, finger grooves, and
   thumb rest to match your hand.
5. **Export** — The model is exported as an STL, ready to slice and print.

## Requirements

- Python 3.10+
- `mediapipe`
- `opencv-python`
- `cadquery`
- A webcam or smartphone camera
- A standard credit/ID card (used as a scale reference)
- A 3D printer (FDM, PLA or PETG recommended)

## Usage

```bash
pip install -r requirements.txt
python capture.py        # guided photo capture
python measure.py        # extract hand measurements from photos
python generate_model.py # produce the parametric STL
```

The generated STL will be saved to `output/shell.stl`.

## Assembly

The exported shell is designed in two halves (top/bottom) with screw bosses.
You'll need:
- An optical mouse sensor module
- Two microswitches (left/right click)
- A scroll wheel assembly
- M2 screws

Assembly notes and wiring diagrams are in `docs/assembly.md`.

## Status

Actively in development. Current version generates a working shell shape;
future work includes support for multiple grip styles (palm/claw/fingertip)
and better handling of edge cases like rings or long nails during hand capture.

## Notes

Measurements are only as accurate as the input photos — good, even lighting
and a hand held flat/still against the camera give the best results.
```


Bill of Materials
#
Item
Qty
Notes
Approx. Source
1
PLA or PETG filament
~60g
For top + bottom shell halves
Any FDM-compatible spool
2
Optical mouse sensor module (e.g. PMW3360 breakout)
1
Handles cursor tracking
Robu.in / Robocraze
3
Microcontroller (e.g. Arduino Pro Micro / ATmega32U4 board)
1
Acts as USB HID mouse
Robu.in / Robocraze
4
Microswitches (left/right click)
2
3-pin, 50M-cycle rated preferred
Robu.in / Robocraze
5
Scroll wheel encoder assembly
1
Salvaged or standalone rotary encoder
Salvaged / Robocraze
6
Tactile side buttons (optional)
0–2
For back/forward buttons
Robu.in
7
M2 machine screws
4–6
Shell assembly
Robu.in
8
M2 heat-set inserts (optional)
4–6
For stronger, reusable screw bosses
Robu.in
9
Micro-USB or USB-C cable
1
Data/power connection
Any
10
Thin foam/silicone pads
2–4
Shell feet, reduces friction on desk
Any
11
Hookup wire (26–30 AWG)
~30cm
Internal wiring
Robu.in

 