# Audio Amplifier: Microphone to Speaker System

A fully analog audio amplification circuit that converts low-level microphone signals (10-20mV peak-to-peak) into speaker-driving output (5V swing, ~3W @ 8Ω). Designed and built with emphasis on noise rejection and real-world analog behavior.

## Overview

This is a complete analog signal chain: microphone input → pre-amplification → gain stage → bandpass filtering → power amplification → 8Ω speaker output. The circuit achieves approximately 500x overall voltage gain through cascaded amplification stages while maintaining excellent noise characteristics.

## Specifications

| Parameter | Value |
|-----------|-------|
| **Input Signal** | 10-20mV peak-to-peak (microphone level) |
| **Output Signal** | 5V swing |
| **Overall Voltage Gain** | ~500x (54dB) |
| **Frequency Response** | 20Hz - 20kHz (bandpass) |
| **Output Power** | ~3W @ 8Ω load |
| **Supply Voltage** | ±15V |
| **Quiescent Current** | ~1mA from input |
| **Load Impedance** | 8Ω (speaker) |

## Architecture

```
Microphone Input (10-20mV)
        ↓
   [Pre-Amplifier]
        ↓
   [Gain Stage] (~40dB gain)
        ↓
   [Bandpass Filter] (20Hz-20kHz)
        ↓
   [Power Amplifier]
        ↓
   Speaker Output (5V swing, 3W @ 8Ω)
```

### Stage Details

**Pre-Amplifier**: Initial low-noise amplification stage to bring microphone-level signals to a usable range.

**Gain Stage (Common-Emitter Amplifier)**: Primary amplification stage providing ~40dB (100x) gain. Implemented with careful biasing to ensure linear operation across the audio frequency range.

**Bandpass Filter**: Removes DC and out-of-band noise while passing the full audio spectrum (20Hz-20kHz). Eliminates low-frequency rumble and high-frequency hiss efficiently.

**Power Amplifier**: Drives the 8Ω speaker load directly from the filtered signal, delivering approximately 3W of output power.

## Components

**Op-Amps**: UA741 (general-purpose voltage amplification)

**Power Transistors**: 
- TIP31A (NPN, for positive half-cycle amplification)
- TIP32A (PNP, for negative half-cycle amplification)

**Supporting Components**: See `bom/amp.bom` for complete bill of materials with part numbers and values.

## Design Approach

This circuit was built with hands-on understanding of analog electronics:

- **Simulation vs. Reality**: Designed in LTspice (schematics in `schematics/`) and then prototyped. The experience revealed important differences between theoretical behavior and real-world component performance—resistor tolerances, parasitic capacitances, and temperature effects all played a role.

- **Component Sensitivity**: The gain stage is particularly sensitive to transistor β (current gain) and biasing resistor values. Fine-tuning these parameters was critical to achieving stable gain and frequency response.

- **Noise Management**: The bandpass filter design was optimized to reject DC offset and out-of-band noise while preserving signal fidelity. Low-impedance nodes were carefully managed to minimize noise pickup.
- 
## Files

- **`schematics/`**: LTspice circuit designs
  - `final.asc` - Complete final design
  - `pre-amp+gain.asc` - Pre-amp and gain stages
  - `preamp-gain-filter.asc` - Pre-amp, gain, and filter stages
  - `poweramp.asc` - Power amplifier stage
  
- **`libraries/`**: Custom component libraries for LTspice
  - `tip31a.lib`, `tip32a.lib`, `UA741.301`
  
- **`bom/`**: Bill of materials with part numbers and values
  
- **`docs/`**: Design documentation
  - `audio-amp-report.pdf` - Detailed design report with measurements, test results, and photos of the prototype

## Key Learnings

- **Analog Component Behavior**: Understanding the gap between simulated and real-world performance, especially with transistors and passive components.
- **Signal Chain Design**: How to cascade amplification stages while managing gain, impedance, and noise at each step.
- **Practical Filtering**: Implementing and tuning bandpass filters for audio applications.
- **Power Delivery**: Designing output stages to drive real loads (8Ω speaker) while maintaining signal quality.

## License

Open for educational and personal use.

---
