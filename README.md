# Project Name

> Espurr - the neuroadaptive companion

## Project Owner

**Name:** Vicky Ji
**Virginia Tech Email:** yutongji@vt.edu

## Project Overview
A few months ago, I had a conversation with a friend on the walk home. I remember how happy I was afterward, but I couldn't tell you a single thing we talked about.

It's strange how the moments I wish I could revisit are usually the ones I never thought to record. And pulling out my phone in the middle of them would have made them feel different anyway.

So I'm building a cat.

ESPURR is a wearable robotic companion named after the Pokémon Espurr. It sits on your head, notices what's happening around you, and reacts through little movements of its ears. I'm using EEG alongside computer vision so its behavior isn't tied to a single sensor or a fixed set of reactions. It doesn't know what you're thinking, and I don't want it pretending that it does.

In companion mode, ESPURR uses its surroundings and physiological signals to decide when to interact or stay quiet. There's also a listening mode where you can talk about your day and save it as a journal entry. When you get home, you place ESPURR on its charging dock and explore the things you've chosen to keep through an interface inspired by Obsidian.

Right now, I've completed the first EEG-to-motion prototype. Recorded Muse 2 signals pass through an FPGA filter on a PYNQ-Z2, where Python running on the ARM processor uses an adaptive detector to control a servo. The camera and listening features are still in development.

I don't want ESPURR to tell people which moments are important. I want it to be a small companion that notices the world with them and gives them a way to look back on the parts they might have missed.


## What I Hope to Learn
I want to learn how to build a robot that can make decisions based on what's happening around it rather than just following predefined commands. ESPURR gives me a chance to work more deeply with embedded hardware and explore how different sensors can influence a robot's behavior. I'm also interested in understanding what makes a robotic companion feel natural to interact with.

## Design and Implementation
ESPURR uses a PYNQ-Z2 board, with FPGA logic handling EEG signal processing and Python running on the ARM processor to make decisions about how the robot responds.

For Stage 1, I built a 101-tap FIR filter and RMS detector in Verilog, connected through AXI DMA. I then developed an adaptive detector in Python that compares EEG activity against a rolling baseline. Using recorded Muse 2 data, I tested the full pipeline and successfully triggered an SG90 servo through an Arduino Uno.

I'm now working toward combining EEG with computer vision so ESPURR can react based on its surroundings rather than relying on brain signals alone. Future development will also include a listening mode for spoken journal entries and a charging dock where users can revisit saved moments through a private, sonder-inspired interface.


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
| PLA filament for enclosure | 1 spool | ~$14.00 | [Amazon](https://www.amazon.com/dp/B0BM7WZPXJ) |
| Electret microphone capsule | 1 | $1.50 | [Adafruit](https://www.adafruit.com/product/1064) |
| 3.5 mm TRRS plug terminal block | 1 | $2.50 | [Adafruit](https://www.adafruit.com/product/2914) |

**Estimated total:** $495.39 USD

## Timeline and Milestones

| Milestone | Target Date | Status |
|---|---|---|
| Stage 1 | Early Nov. | Complete |
| Stage 2 | TBD | In Progress |

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

### 2026-10-22
Completed and verified the 101-tap P300 lowpass FIR filter in Vivado. Passed frequency-response tests at 5–25 Hz, matched all 101 impulse-response outputs and 300 Python reference outputs, and verified reset, saturation, and output-valid timing. Began implementing the AXI4-Stream wrapper for DMA integration with the PYNQ-Z2.

### 2026-11-03
Finished the AXI4-Stream wrapper and connected the 101-tap FIR filter to AXI DMA on the PYNQ-Z2. Tested the full pipeline on hardware and matched all 300 outputs with Python. Cleaned up the old FIR3 and GPIO connections, regenerated the bitstream, and passed timing at 50 MHz with +6.870 ns slack.

Loaded real Muse 2 EEG from the HEROIC dataset and resampled it from 256 Hz to 100 Hz for FPGA processing. Tested 2,000 EEG samples through the AXI DMA and FIR101 pipeline on the PYNQ-Z2, matching all 2,000 outputs with Python. Analyzed EEG activity using a 0.5-second RMS window and tested a 20 µV threshold detector, identifying three activity events in the 20-second recording. 

### 2026-11-05
Stage 1 Complete.
Connected FIR101, AXI DMA, RMS detector, and event counter on PYNQ-Z2.
Fixed timing issues by pipelining the RMS detector (WNS: +4.032 ns at 50 MHz).
Tested recorded Muse 2 EEG triggering an SG90 servo through Arduino Uno.
Built a Python adaptive detector with rolling baseline, artifact filtering, and cooldown.
Tested two EEG recordings and verified 2000/2000 matching outputs across DMA transfers. Example picture below.

### YYYY-MM-DD
Describe what you worked on, what was completed, any problems you encountered, and what you plan to work on next.

## Project Files
<img width="1278" height="707" alt="image" src="https://github.com/user-attachments/assets/f2c33960-5af1-418e-9c8b-72b6acf90280" />
<img width="630" height="256" alt="image" src="https://github.com/user-attachments/assets/b1e6f25b-9c9a-4a4a-8917-80194e9d51d9" />
<img width="579" height="799" alt="image" src="https://github.com/user-attachments/assets/47a1ce58-38bc-4366-ae68-f64d072cae92" />


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
Sample dataset for eeg input tests (muse 2) : https://zenodo.org/records/11493897 
