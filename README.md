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

| Item | Qty. | Estimated cost | Link |
| --- | ---: | ---: | --- |
| PYNQ-Z2 FPGA + ARM board | 1 | $158.90 | [Newark](https://www.newark.com/tul-corporation/1m1-m000127dev/tul-pynq-z2/dp/13AJ3027) |
| Muse 2 EEG headband | 1 | $249.99 | [Muse](https://choosemuse.com/products/muse-2) |
| OV5640 camera breakout | 1 | $12.50 | [Adafruit](https://www.adafruit.com/product/5839) |
| SG92R micro servos for ears | 2 | $11.90 | [Adafruit](https://www.adafruit.com/product/169) |
| 8 Ω, 1 W mini speakers (four-pack; one used initially) | 1 pack | ~$8.00 | [Amazon](https://www.amazon.com/dp/B0CJNB3CR2) |
| PAM8302 analog audio amplifier | 1 | $3.95 | [Adafruit](https://www.adafruit.com/product/2130) |
| C&K three-position mode switch | 1 | $11.15 | [DigiKey](https://www.digikey.com/en/products/detail/c-k/A10303RNZQ/2055100) |
| 32 GB microSD card | 1 | ~$21.00 | [Amazon](https://www.amazon.com/dp/B010Q57T02) |
| PLA filament for enclosure | 1 spool | ~$14.00 | [Amazon](https://www.amazon.com/dp/B0BM7WZPXJ) |
| Electret microphone capsule | 1 | $1.50 | [Adafruit](https://www.adafruit.com/product/1064) |
| 3.5 mm TRRS plug terminal block | 1 | $2.50 | [Adafruit](https://www.adafruit.com/product/2914) |

**Estimated total:** $495.39 USD

The PYNQ-Z2 and one servo are needed for the initial FPGA-processing prototype. The Muse 2, camera, audio components, external mode switch, and enclosure materials can be purchased in stage 2. My computer will power the FPGA and the servo at the moment.

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
### 2026-10-06 
Received the PYNQ, did initial setup with flashing .img onto board and ARM/Linux access verified over UART.

### 2026-10-08
Verified ARM-FPGA communication through built in LED control and switches. Implemented and visualized a synthetic EEG processing pipeline using amplitude-based (RMS) event detection with FPGA-controlled LED responses activated only when consent was enabled. 

### 2026-10-09
Configured Vivado 2025.2 for the PYNQ-Z2 and developed an initial 3-tap FIR filter in Verilog to prepare for larger tap FIR filters for EEG. Learned FPGA filtering fundamentals like FIR coefficients, bit-width management, and sample-valid control.

### 2026-10-14
Implemented and validated a custom Zynq-7000 AXI GPIO hardware design in Vivado, completing synthesis, implementation, and bitstream generation. Successfully deployed the custom overlay to the PYNQ-Z2 and verified ARM–FPGA communication by controlling a physical LED through Python.

### 2026-10-15
Integrated the 3-tap FIR filter into the PYNQ-Z2 Block Design using AXI GPIO for data and control signals. Verified sample-valid logic through simulation and successfully validated the hardware design in Vivado.

### 2026-10-16
Designed and validated a 101-tap 8–13 Hz FIR bandpass filter in Python using a Hamming window and simulated EEG signals. Converted coefficients to 16-bit Q1.15 fixed-point format and exported them for Vivado. Initialized the Verilog FIR module with coefficient storage, sample buffering, and sequential sample accumulated architecture.

### 2026-10-18
Finished the 101-tap EEG alpha-band FIR filter in Verilog using a sequential MAC, Q1.15 coefficients, and output saturation. Verified all 101 impulse-response outputs in Vivado, confirming that the filter correctly stores previous samples and performs the fixed-point accumulated (from past samples) calculations. Going to test if 101-tap FIR passes frequencies inside the alpha band and attenuates frequencies outside it next. After that AXI DMA integration.

### YYYY-MM-DD
Describe what you worked on, what was completed, any problems you encountered, and what you plan to work on next.

## Project Files
<img width="927" height="574" alt="image" src="https://github.com/user-attachments/assets/f8a40aa3-bedb-4fd6-a8fd-fcb3bd6dae6a" />

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
