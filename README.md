<img width="499" height="344" alt="Screenshot 2026-08-03 171317" src="https://github.com/user-attachments/assets/4a281c9f-f4d2-4539-9451-8743e6cfecda" />
# ERGOmouse
# ErgoMouse

# Devlog 1 — Why does every mouse hurt my wrist?

Started actually planning this today instead of just complaining about it. My wrist has been aching after long coding sessions for months, and I finally admitted it's probably the mouse, not just "too much screen time." Did some digging and it turns out generic mice are designed around an "average" hand that doesn't really exist — everyone's palm width, finger length, and thumb position are different, but every mouse on the shelf is the same shape for everyone.

Spent a good chunk of the afternoon reading about ergonomics — carpal tunnel syndrome, ulnar deviation, the whole "pronation" thing where your forearm has to twist unnaturally to grip a flat mouse. Looked at existing ergonomic mice like the Logitech MX Vertical and the Anker vertical mouse. They're better than a standard mouse, but they're still one-size-fits-all — just a different fixed shape instead of the flat one. Nobody's actually mass-producing a mouse molded to an individual hand, probably because doing that at scale is expensive and impractical.

That's basically the idea I want to chase: what if you could take a few photos of your hand, and software could turn that into a 3D-printable mouse shell shaped specifically for you?

Brainstormed a feature list for a while:
- Photo-based hand capture (no scanner or fancy hardware needed)
- Automatic extraction of key measurements — palm width, finger lengths, thumb rest position
- A parametric CAD model that adjusts based on those measurements
- Exportable STL for 3D printing
- Standard mouse internals (sensor, switches) fitted into the custom shell

For tech choices, I'm leaning toward Python for the image processing since MediaPipe has a hand-landmark model that's already solid out of the box, and I don't want to train my own from scratch this early. For the CAD side I'm debating between generating geometry programmatically with something like CadQuery/OpenSCAD versus hand-modeling in Fusion 360 with parameters exposed. Programmatic wins for automation, so that's probably the direction.

Rough architecture in my head right now:
1. Image capture UI with on-screen hand-positioning guides
2. Landmark detection + measurement extraction
3. Measurement → parametric model mapping
4. STL export
5. (later) assembly instructions for the electronics

Biggest open question: how forgiving does the photo-taking process need to be for the measurements to still be usable? If a user's hand is slightly rotated or the lighting is bad, does the whole model fall apart? That's tomorrow's problem.

---

# Devlog 2 — Turning hand photos into numbers

Today was all about the image-processing pipeline, and it was messier than I expected.

Got MediaPipe Hands running and pulling the 21 landmark points per hand pretty reliably in good lighting. The instructions screen now asks for two photos: palm flat on a table, fingers spread, and a side profile shot to get thumb height. From the landmarks I'm calculating:

- **Palm width**: distance between the index and pinky MCP joints (landmarks 5 and 17)
- **Finger lengths**: sum of the segment distances from each fingertip landmark down to its base knuckle
- **Thumb position**: angle and offset of the thumb CMC joint relative to the palm centerline, taken from the side profile shot

The tricky part was scale. Landmarks come back as normalized coordinates, not real-world millimeters, so I needed a reference object in frame. Went with "place a standard credit card next to your hand" — it's a fixed, known size (85.6mm x 53.98mm) most people have on hand, and I can detect its edges with OpenCV to establish a pixel-to-mm ratio.

Once I had real measurements, I moved on to the parametric model in CadQuery. Built a base mouse shell as a set of parameters — palm cradle width, palm cradle length, thumb rest angle, finger groove depth — and wired the extracted measurements into those parameters. First few generated shells looked more like potatoes than mice, so I spent a few hours adjusting the base spline curves so the palm cradle actually follows a believable hand contour instead of just scaling a box.

Problems today:
- Bad lighting or a shadow across the palm throws off landmark confidence — added a confidence threshold that rejects the photo and asks the user to retake it
- Rings and long nails were shifting the fingertip landmarks slightly — not fixing this yet, just noting it
- First parametric attempts didn't leave room for the mouse's internal electronics (sensor board, switches) — had to add a fixed-size internal cavity that the palm cradle geometry works around instead of just shrink-wrapping the hand shape directly

Next up: experimenting with a few different shell shape families (relaxed claw grip vs. palm grip) so the software can pick a base shape template before applying the personalized measurements.

---

# Devlog 3 — First real print, and reality check time

Big day — printed the first shell today. Exported the STL from CadQuery, sliced it, and sent it to the printer. It took about 4.5 hours to print in PLA, and the wait was brutal.

The fit was... close, but not right. The palm cradle was actually pretty comfortable, but the thumb rest sat too far forward, and my pinky kept sliding off the side groove. Went back through the measurement math and realized the thumb angle calculation from the side-profile photo was off — I was measuring from the wrist landmark instead of the thumb CMC joint, which threw the whole angle calc by a good 10-15 degrees. Fixed the landmark reference and regenerated the model.

Also spent time today fitting actual mouse internals into the shell — a basic optical sensor module, two microswitches for left/right click, and a scroll wheel assembly salvaged from an old mouse. Had to redesign the internal cavity walls to leave clearance for the PCB and battery, and added screw bosses so the top and bottom shells can actually be assembled instead of just glued.

Things I learned the hard way:
- A model that looks right on screen doesn't mean it feels right in your hand — print-and-test iteration is non-negotiable, no amount of staring at the CAD viewport substitutes for actually holding it
- Wall thickness matters a lot for print strength — my first version had 1.2mm walls in the thumb area and it cracked when I tightened the assembly screws; bumped it to 2mm
- Button placement needs its own pass — I'd been treating the shell as one shape-fitting problem, but click actuation force and finger reach are a separate ergonomics problem layered on top

Printed version two tonight with the corrected thumb angle and thicker walls. Fit is noticeably better — pinky groove finally holds, thumb rest feels natural. Still want to test with a couple other people's hands tomorrow to make sure this isn't just tuned to my own hand by accident.

---

# README.md

```markdown
# HandFit Mouse

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


 