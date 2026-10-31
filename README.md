# HCL-ABES-3rdYear-Edge_voice_Mfcc-
RTL, Testbench, constraints, dataset analysis 
# EdgeVoice: Real-Time MFCC Accelerator for On-Device Speech Processing

An FPGA-based hardware accelerator for extracting Mel-Frequency Cepstral Coefficients (MFCCs) from audio signals using fixed-point digital signal processing.

> **Project Status:** Work in Progress 🚧

## Overview

EdgeVoice aims to implement a hardware-efficient MFCC extraction pipeline for real-time speech processing applications such as wake-word detection, voice assistants, and edge AI devices.

The design uses Verilog/SystemVerilog RTL and targets the **Digilent Zybo Z7-20 (Zynq-7000)** FPGA development board.

## Target Hardware

- **FPGA Board:** Digilent Zybo Z7-20
- **FPGA Device:** XC7Z020-1CLG400C
- **Development Tool:** Xilinx Vivado
- **Design Language:** Verilog / SystemVerilog
- **Clock Frequency:** 50 MHz (design target)
- **Arithmetic:** Fixed-point

## System Specifications

| Parameter | Specification |
|---|---|
| Audio input | Signed 16-bit mono PCM |
| Sampling frequency | 16 kHz |
| Frame size | 256 samples |
| Window function | Hamming |
| FFT size | 256 points |
| Spectrum | Magnitude squared |
| Mel filter bank | 20 filters |
| Log compression | Fixed-point approximation |
| MFCC output | 13 coefficients |

## Architecture

The intended processing pipeline consists of:

1. **Frame Buffer** – Stores 256 incoming audio samples.
2. **Hamming Window** – Applies a window function to reduce spectral leakage.
3. **256-Point FFT** – Converts the windowed time-domain samples into the frequency domain.
4. **Magnitude Squared** – Calculates the power spectrum using real² + imaginary².
5. **Mel Filter Bank** – Applies 20 Mel-spaced filters to the power spectrum.
6. **Log Compression** – Applies logarithmic compression to Mel energies.
7. **DCT** – Generates 13 MFCC coefficients.

## Repository Structure

```text
EdgeVoice/
├── rtl/
│   ├── edgevoice_mfcc_top.v
│   ├── frame_buffer.v
│   ├── hamming_window.v
│   ├── fft256_radix2.v
│   ├── magnitude_squared.v
│   ├── mel_filterbank.sv
│   ├── log_compress.v
│   └── dct13.sv
├── sim/
│   ├── tb_frame_buffer.v
│   ├── tb_hamming_window.v
│   ├── tb_fft256_radix2.v
│   ├── tb_magnitude_squared.v
│   ├── tb_mel_filterbank.sv
│   ├── tb_log_compress.v
│   └── tb_dct13.sv
├── constraints/
├── scripts/
├── README.md
└── LICENSE
```

*Update this structure to match the actual files committed to the repository.*

## Tools Required

- Xilinx Vivado Design Suite
- Verilog/SystemVerilog simulator (Vivado XSim)
- Python 3 (for reference-model development and verification)

## Getting Started

1. Clone this repository:

   ```bash
   git clone https://github.com/YOUR_USERNAME/EdgeVoice.git
   ```

2. Open Vivado.
3. Open the Tcl Console.
4. Navigate to the project directory.
5. Run the project creation script:

   ```tcl
   source scripts/create_project.tcl
   ```

6. Run behavioral simulation after selecting the required testbench as the simulation top.

## Verification

Individual testbenches are provided for the main processing blocks.

| Testbench | Module |
|---|---|
| tb_frame_buffer.v | Frame Buffer |
| tb_hamming_window.v | Hamming Window |
| tb_fft256_radix2.v | FFT |
| tb_magnitude_squared.v | Magnitude Squared |
| tb_mel_filterbank.sv | Mel Filter Bank |
| tb_log_compress.v | Log Compression |
| tb_dct13.sv | DCT |

**Note:** Testbench presence does not imply successful verification. Simulation results and numerical comparison against a Python reference model will be documented as verification is completed.

## Future Improvements

- Complete and integrate all MFCC processing blocks.
- Verify FFT, Mel filter bank and DCT numerical accuracy.
- Develop a Python-based golden reference model.
- Perform end-to-end simulation with audio test vectors.
- Run FPGA synthesis and implementation.
- Analyze resource utilization, timing and power.
- Integrate audio input/output with the Zybo Z7-20 board.

## Applications

- Voice activity detection
- Wake-word detection
- Speech recognition preprocessing
- Low-power edge AI systems
- Real-time audio signal processing

## Author

**YOUR NAME**

GitHub: [YOUR GITHUB PROFILE](https://github.com/YOUR_USERNAME)

---

*EdgeVoice is an educational FPGA/DSP project focused on hardware acceleration of MFCC feature extraction.*
