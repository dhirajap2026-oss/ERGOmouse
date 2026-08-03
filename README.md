<img width="499" height="344" alt="Screenshot 2026-08-03 171317" src="https://github.com/user-attachments/assets/4a281c9f-f4d2-4539-9451-8743e6cfecda" />
# ERGOmouse
# ErgoMouse
 

# ERGOmouse

ERGOmouse is an open-source project focused on creating a truly personalized ergonomic computer mouse. Instead of forcing users to adapt to a standard mouse shape, ERGOmouse generates a custom 3D-printable shell based on photos of the user's hand. The goal is to improve comfort, reduce wrist strain, and make long-term computer use more comfortable.

## Why I Started This Project

Most mice are designed to fit as many people as possible, but everyone's hand is different. After spending long hours using a computer, I became interested in whether a mouse could be designed specifically for an individual's hand rather than using a one-size-fits-all approach.

This project combines computer vision, parametric CAD generation, and custom hardware to explore that idea.

## Features

- Generate a custom mouse shell from hand photos.
- Parametric 3D model generation.
- STL export for 3D printing.
- Modular internal design for electronics.
- Open-source development.

## Planned Workflow

1. Capture multiple photos of the user's hand.
2. Detect key landmarks and measurements.
3. Generate a parametric 3D model.
4. Export an STL file.
5. Print the shell.
6. Assemble the electronics.
7. Test and improve the design.

## Hardware

Planned hardware includes:

- ESP32
- Optical mouse sensor
- Rotary encoder (optional)
- Kailh switches
- Custom PCB
- USB-C connection
- 3D printed enclosure

## Software

The software will:

- Guide the user through taking hand photos.
- Process the images.
- Extract important measurements.
- Generate a customized mouse shell.
- Export the final model as an STL file.

## Project Status

This project is currently in active development.

Current work includes:

- PCB design
- Mechanical design
- Software planning
- Prototype development

## Repository Structure

```
ERGOmouse/
├── README.md
├── journals/
├── hardware/
├── software/
├── pcb/
├── cad/
└── images/
```

## Roadmap

- [ ] Complete image-processing pipeline
- [ ] Generate first parametric mouse shell
- [ ] Finish PCB design
- [ ] Print first prototype
- [ ] Assemble electronics
- [ ] Test ergonomics
- [ ] Improve shell design
- [ ] Release first public version

## License

This project is licensed under the MIT License.

---

This project is being developed as a learning experience while exploring ergonomic hardware design, computer vision, PCB design, and 3D printing.


