<img width="499" height="344" alt="Screenshot 2026-08-03 171317" src="https://github.com/user-attachments/assets/4a281c9f-f4d2-4539-9451-8743e6cfecda" />
# ERGOmouse
# ErgoMouse

> **An open-source ergonomic mouse built for comfort first.**
>
> *One mouse. Every hand. Limitless comfort.*

---

## Why ErgoMouse?

Most computer mice are designed to fit as many people as possible. That means they rarely fit anyone perfectly.

ErgoMouse is a personal project focused on creating a mouse that naturally fits the hand, reduces strain, and remains comfortable during long hours of work or gaming.

The project begins by designing the ideal mouse for my own hand. The long-term vision is to make personalized ergonomic mice accessible to everyone.

---

## Vision

The future of ErgoMouse is personalized ergonomics.

The planned software will allow users to:

* 📷 Upload a photo of their hand holding their current mouse.
* ✋ Upload a photo of their hand in a relaxed, comfortable position.
* 🤖 Generate a custom ergonomic shell based on their hand shape.
* 🖨️ Download and 3D print the shell at home.

Instead of adapting your hand to the mouse, the mouse adapts to your hand.

---

## Current Goals

* Design an ergonomic shell
* Prototype using 3D printing
* Test different grip styles
* Optimize comfort and weight
* Develop custom PCB
* Build open-source firmware
* Document every stage of development

---

## Roadmap

### Phase 1 — Research

* [x] Project idea
* [x] Initial sketches
* [x] CAD design
* [ ] Ergonomic testing

### Phase 2 — Prototype

* [ ] 3D printed shell
* [ ] Button placement
* [ ] Scroll wheel integration
* [ ] Internal mounting system

### Phase 3 — Hardware

* [ ] PCB design
* [ ] Sensor integration
* [ ] Firmware
* [ ] USB/Wireless support

### Phase 4 — Open Source Release

* [ ] Complete build guide
* [ ] STL files
* [ ] CAD source files
* [ ] PCB files
* [ ] Assembly instructions

### Phase 5 — AI Shell Generator

* [ ] Hand image analysis
* [ ] Automatic shell generation
* [ ] Personalized ergonomic recommendations
* [ ] Printable custom shell export

---

## Technologies

* CAD (Fusion 360 / FreeCAD)
* 3D Printing
* Embedded Electronics
* PCB Design
* Firmware Development
* Computer Vision *(planned)*
* AI-Assisted Design *(planned)*

---

## Repository Structure

```text
docs/           Documentation and devlogs
cad/            CAD source files
stl/            Printable models
electronics/    PCB and schematics
firmware/       Mouse firmware
software/       Future desktop application
assets/         Images and renders
```

---

## Development Philosophy

ErgoMouse is built around one principle:

> **Comfort is not a feature—it is the foundation.**

Every prototype is tested, refined, and improved with ergonomics as the highest priority.

---

## Contributing

Contributions, feedback, ergonomic ideas, and testing suggestions are welcome.

Whether you're a designer, maker, firmware developer, or ergonomics enthusiast, your input can help improve the project.

---

## Development Log

Project updates are published regularly inside the `docs/devlogs/` directory.

---

## License

This project will be released under the MIT License unless otherwise specified.

---

## Follow the Journey

This repository documents the complete journey—from the first sketch to a fully functional ergonomic mouse and, eventually, a platform that enables anyone to create a mouse tailored to their own hand.

If this project interests you, consider starring the repository and following its progress.




## Bill of Materials (Prototype v1)

| Component                    | Quantity | Purpose                                 |
| ---------------------------- | :------: | --------------------------------------- |
| 3D Printed Shell             |     1    | Ergonomic outer housing                 |
| Top Cover                    |     1    | Upper shell with button cutouts         |
| Bottom Plate                 |     1    | Base of the mouse                       |
| Optical Sensor               |     1    | Tracks mouse movement                   |
| Microcontroller              |     1    | Processes inputs and controls the mouse |
| Left Mouse Switch            |     1    | Left-click button                       |
| Right Mouse Switch           |     1    | Right-click button                      |
| Middle Mouse Switch          |     1    | Scroll-wheel click                      |
| Scroll Wheel                 |     1    | Scrolling                               |
| Scroll Wheel Encoder         |     1    | Detects wheel rotation                  |
| USB-C Connector              |     1    | Wired connection and power              |
| PCB                          |     1    | Connects all electronic components      |
| Mouse Feet (PTFE)            |    4–6   | Smooth movement across surfaces         |
| Screws (M2/M2.5)             |    4–6   | Assemble the mouse                      |
| Side Buttons *(Optional)*    |     2    | Forward/Back navigation                 |
| RGB LEDs *(Optional)*        |    1–4   | Status or lighting effects              |
| Battery *(Wireless Version)* |     1    | Power source                            |
| Wireless Module *(Future)*   |     1    | Bluetooth/2.4 GHz connectivity          |

### Tools Required

* 3D Printer
* Soldering Iron
* Solder Wire
* Small Phillips Screwdriver
* Tweezers
* Flush Cutters
* Computer for firmware flashing
* Calipers (recommended)

### Estimated Prototype Cost

| Item                          | Estimated Cost (USD) |
| ----------------------------- | -------------------: |
| Electronics                   |               $20–35 |
| 3D Printed Parts              |                $5–10 |
| Hardware (Screws, Feet, etc.) |                $5–10 |
| **Total**                     |           **$30–55** |

> **Note:** The bill of materials will evolve as the design is refined. Exact part numbers and suppliers will be added once the prototype hardware is finalized.

