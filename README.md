# ADC-and-Serial-Interface
ADC module and serial interface to Matlab
# USB Oscilloscope using MSP430 & MATLAB

This project implements a low-cost, real-time oscilloscope using the **MSP430G2553** microcontroller's ADC10 module and **MATLAB App Designer** for data visualization.

## Overview

- **Platform:** MSP430G2553, MATLAB App Designer
- **Purpose:** Digitize analog signals and visualize them in real-time on a PC.
- **Communication:** UART (115200 baud) via USB.

## Key Features

- ADC10 10-bit sampling (truncated to 8 bits for transmission)
- Real-time waveform plotting using MATLAB GUI
- UART serial communication (bidirectional)
- MATLAB “Start” and “Shutdown” buttons
- On-chip timer for future time-axis calibration
- Sampling Rate: ~11.5 kHz (effective)

## How It Works

1. **MSP430 Microcontroller**
   - Continuously samples an analog input (P1.4) using ADC10 in repeat-single-channel mode.
   - Data is transmitted over UART to MATLAB when MATLAB sends a trigger signal (`'U'`).
   - Transmission done in 8-bit chunks (2 LSBs discarded).
   - Troubleshooting LED (P1.0) turns on/off to indicate sampling/transmission states.

2. **MATLAB App**
   - Designed with App Designer.
   - Contains UIAxes for plotting and buttons to control acquisition.
   - Triggers sampling by writing `'U'` to serial port.
   - Plots 400 samples per session in volts (0–3.3 V range).

## Limitations

- Effective bandwidth ~5.75 kHz (Nyquist limit)
- GUI blocks during acquisition (to be improved using callbacks)
- No native x-axis time calibration (future work: timer integration)

## Future Improvements

- Timer-based sampling interval encoding
- Asynchronous MATLAB callbacks
- ADC resolution preservation (send 10 bits with packing)
- Auto-trigger functionality for edge detection

## Author

**Michael Zhang**  
Engineering Physics, McMaster University  
[LinkedIn](https://www.linkedin.com/in/michael-zhang-077306154)

## References

- [MSP430x2xx User Guide (TI)](https://www.ti.com/lit/ug/slau144k/slau144k.pdf)
- [MSP430G2553 Datasheet](https://www.ti.com/lit/ds/symlink/msp430g2553.pdf)
- [Nyquist Limit – ScienceDirect](https://www.sciencedirect.com/topics/engineering/nyquist-limit)


