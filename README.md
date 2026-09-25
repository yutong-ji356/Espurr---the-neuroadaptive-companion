# Project Name

> Espurr - the neuroadaptive companion

## Project Owner

**Name:** Vicky Ji
**Virginia Tech Email:** yutongji@vt.edu

## Project Overview

Espurr is a prototype wearable, cat-like companion that explores how EEG, embedded hardware, and AI could help people capture and revisit meaningful moments. A Muse 2 headset streams EEG and motion data to a PYNQ-Z2, where FPGA logic processes the signals and detects changes that may prompt a capture. The board’s ARM processor coordinates the system, enforcing a physical OFF, MEMORY, or COMPANION mode before using a camera and microphone to collect context. AI services can interpret the captured image and transcript, while a memory system stores moments so they can be searched and explored through a web app.
The goal is to build and evaluate a consent-aware, end-to-end prototype that combines real-time FPGA signal processing with an AI companion and searchable personal memory. EEG events are treated only as possible capture cues; the project does not claim to read thoughts or identify emotions.

## What I Hope to Learn

Through this project, I hope to gain hands-on experience designing a complete embedded system that combines real-time signal processing, software, and physical interaction.
- FPGA design and hardware/software co-design: Build an FPGA pipeline to filter EEG samples, track a baseline, and send event scores to the ARM processor. Compare the FPGA implementation with software processing on the ARM.
- ARM-based embedded systems: Use Linux on the Zynq ARM processor to receive headset data, enforce consent settings, manage camera and audio capture, and communicate with the project’s backend.
- Signal processing for biosensing: Test EEG preprocessing and event-detection methods using prerecorded data first, then evaluate them with live EEG while accounting for signal quality and motion.
- System integration: Connect the EEG headset, FPGA, camera, microphone, speaker, ear servos, and memory system into a working wearable prototype.

## Design and Implementation

<img width="1343" height="752" alt="image" src="https://github.com/user-attachments/assets/8fe8a831-b5d5-4fc6-ac15-160a696d057b" />

## Bill of Materials

Document the major components and materials used for the project.

| Item | Quantity | Estimated Cost | Link |
|---|---:|---:|---|
| Component | 1 | $0.00 | Link |


| Item | Qty. | Estimated cost | Link |
|---|---:|---:|---|
| PYNQ-Z2 FPGA + ARM board | 1 | $129 | [AMD / TUL](https://www.amd.com/en/corporate/university-program/aup-boards/pynq-z2.html) |
| Muse 2 EEG headband | 1 | $249.99 | [Muse official store](https://choosemuse.com/products/muse-2) |
| USB webcam with built-in microphone (Logitech C270) | 1 | $20–30 | [Logitech](https://www.logitech.com/en-us/shop/p/c270-hd-webcam) |
| Micro servos for cat ears | 2 | $10–14 | [Adafruit SG92R micro servo](https://www.adafruit.com/product/169) |
| Small 8 Ω speaker | 1 | $3–5 | [Adafruit mini oval speaker](https://www.adafruit.com/product/4227) |
| I²S audio amplifier (MAX98357A) | 1 | $6–8 | [Adafruit](https://www.adafruit.com/product/3006) |
| Physical 3-position mode switch | 1 | $3–5 | [Adafruit switch options](https://www.adafruit.com/category/15) |
| 32 GB microSD card | 1 | $10–15 | [Adafruit](https://www.adafruit.com/product/6010) |
| USB Bluetooth adapter compatible with Linux/BlueZ | 1 | $10–15 | [Adafruit Bluetooth USB module](https://www.adafruit.com/product/1327) |
| Regulated 5 V battery/power supply for servos | 1 | $15–25 | [Adafruit power options](https://www.adafruit.com/category/583) |
| 3D-printing material for enclosure | 1 | $5–14 | [Elegoo PLA filament]([https://www.adafruit.com/product/2060](https://www.amazon.com/ELEGOO-Filament-Dimensional-Accuracy-Compatible/dp/B0BM7WZPXJ/ref=sr_1_3_pp?crid=2HU04TCQXMW8K&dib=eyJ2IjoiMSJ9.UNY88SKHgPiEdWlM37-CK_TM2wMtcLhUGFFQw5hSt5AJOXR1Z-TD3bfe85BZtuiPwzMRn2LlUjWodXN2SgqAMf-nBc9cYgtPllDw7nVe8CpcAPJAJBb8BM6lqzjae6ayU0Ua6e8XQIHPFKUPFJBGmadoCnEhafF7sxTd7SbebaR-6ZLFXAllnaBik5fjYu2uHI5zcD-ebJ2qn-wodhZ11OzWamaeBlhG1nBkoZKUufw.wb0-5leUgJBbyKT2iKltu3V9hlxBbDvxXpVXQNTtn2g&dib_tag=se&keywords=elegoo+filament+pla&qid=1790365920&sprefix=elegoo+fil%2Caps%2C256&sr=8-3)) |


**Estimated Total Cost:** $0.00

## Timeline and Milestones

Outline the major stages of the project and update them as work progresses.

| Milestone | Target Date | Status |
|---|---|---|
| Project planning | Date | Not Started |
| Initial design | Date | Not Started |
| Prototype | Date | Not Started |
| Testing | Date | Not Started |
| Project completion | Date | Not Started |

## Progress Log

Use this section to document meaningful progress throughout the project.

### YYYY-MM-DD

Describe what you worked on, what was completed, any problems you encountered, and what you plan to work on next.

## Project Files

Organize and document important project files in this repository. Depending on the project, this may include:

- Source code
- KiCad files
- Schematics
- PCB layouts
- CAD files
- Datasheets
- Test results
- Documentation

## Useful Links

Add any references, datasheets, documentation, tutorials, or other resources relevant to the project.

## Project Image

Replace the `hero.png` file in the root of this repository with an image representing your project.

**Keep the filename as `hero.png`.**

This image is used as the project cover image on the AMP Lab website.
