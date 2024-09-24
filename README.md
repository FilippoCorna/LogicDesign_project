# LogicDesign_project
Hardware level design of logical functions

# VHDL Project: Convolutional Encoder

## Project Overview

This project implements a hardware module described in VHDL that interfaces with a memory component to process a sequence of input bytes. The module encodes the input data using a convolutional coding scheme, generating a serialized output that is stored back in memory. 

## Specifications

- The module receives a continuous sequence of W words, each 8 bits in length, and outputs a continuous sequence of Z words, each also 8 bits.
- The input sequence is serialized into a continuous bitstream (U), which is then encoded using a 1/2 convolutional code, producing an output bitstream (Y).
- The length of the input stream U is `8 * W`, while the length of the output stream Y is `8 * W * 2`, resulting in `Z = 2 * W`.
- The design includes a finite state machine (FSM) with the initial state labeled `00`, processing input and generating output according to specified transitions.

## Functional Description

### Input/Output Signals

- **Inputs:**
  - `i_clk`: Clock signal.
  - `i_rst`: Reset signal to initialize the module.
  - `i_start`: Start signal to begin processing.
  - `i_data`: Input data signal from memory.

- **Outputs:**
  - `o_address`: Address output for memory access.
  - `o_done`: Signal indicating the completion of processing.
  - `o_en`: Enable signal for memory operations.
  - `o_we`: Write enable signal for memory write operations.
  - `o_data`: Output data signal sent to memory.

### Memory Interface

The memory is assumed to be instantiated within the provided test bench. The first byte of the sequence (W) is stored at memory address `1`, and the output data (Z) begins storing at address `1000`.

## Examples

### Example 1: Sequence Length 2

- **Input:** `W: 10100010 01001011`
- **Output:** `Z: 11010001 11001101 11110111 11010010`
  
### Example 2: Sequence Length 6

- **Input:** `W: 10100011 00101111 00000100 01000000 01000011 00001101`
- **Output:** `Z: 11010001 11001110 ...`

## Implementation Details

- The project is implemented using Xilinx Vivado Webpack for synthesis.
- The target FPGA can be any suitable device; however, the Artix-7 (xc7a200tfbg484-1) is recommended.
- The system is designed to operate with a clock period of at least 100 ns.
