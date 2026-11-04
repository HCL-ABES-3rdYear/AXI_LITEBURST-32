# AXI-LiteBurst-32

## Project Overview

AXI-LiteBurst-32 is a modular Verilog RTL project that demonstrates a 32-bit AXI4-Lite-style memory-mapped slave interface. It includes read and write channel handling, address decoding, byte-strobe memory writes, response generation, and low-power idle monitoring.

The design is developed using AMD/Xilinx Vivado. The block diagram below illustrates the overall system architecture and its major functional components.

## Block Diagram

![AXI-LiteBurst-32 Block Diagram](screenshots/Block_Diagram.png)

## Key Features

- 32-bit data path with parameterized 8-bit address width.
- Five AXI4-Lite channels: AW, W, B, AR, and R.
- Internal memory of 16 × 32-bit words (64 bytes).
- Byte-level write control using `WSTRB[3:0]`.
- Read and write address decoding.
- Separate read and write datapaths.
- Read and write response generation.
- Low-power idle monitoring with activity detection.
- Standalone burst-style sequencer supporting 1–16 beats with 4-byte address increments.

## RTL Modules

| Module | Description |
|---|---|
| `axi_liteburst32_top.v` | Top-level design |
| `axi_aw_channel.v`, `axi_w_channel.v`, `axi_b_channel.v` | Write channel logic |
| `axi_ar_channel.v`, `axi_r_channel.v` | Read channel logic |
| `address_decoder.v` | Address decoding |
| `write_data_path.v`, `read_data_path.v` | Read/write datapaths |
| `response_generator.v` | Response generation |
| `low_power_controller.v` | Idle and activity monitoring |
| `burst_controller.v` | Burst-style address sequencer |
| `axi_slave_fsm.v`, `reg_mem_bank.v` | Additional standalone modules |

## Design Specifications

| Parameter | Value |
|---|---|
| HDL | Verilog |
| Top Module | `axi_liteburst32_top` |
| Address Width | 8 bits (parameterized) |
| Data Width | 32 bits |
| Internal Memory | 16 × 32-bit words |
| Write Strobes | 4 bits |
| Reset | Active-low synchronous |
| Burst Sequencer Length | 1–16 beats |

## Working Principle

**Write Operation:** The write address and write data channels receive the address and data from the master. The address decoder selects the target location, while the write datapath handles data and byte strobes. The response generator produces the write response.

**Read Operation:** The read address channel receives the requested address. The decoder selects the memory location, and the read datapath retrieves the data and sends it through the read response channel.

**Low-Power Monitoring:** The low-power controller monitors interface activity and generates a clock-enable suggestion during idle conditions.

## Simulation

1. Open `AXI_LiteBurst32.xpr` in Vivado.
2. Set `tb_axi_liteburst32_top` as the simulation top.
3. Select **Run Simulation → Run Behavioral Simulation**.
4. Verify the simulation transcript and waveforms.

The project includes 14 Verilog testbenches. Run them in Vivado/XSim before reporting test results.

## Important Notes

- AXI4-Lite does not support native burst transactions. The burst controller is a custom sequencer for successive single-beat transfers.
- `burst_controller.v`, `axi_slave_fsm.v`, and `reg_mem_bank.v` are standalone modules and are not instantiated in the supplied top-level design.
- The low-power controller provides activity monitoring and a clock-enable suggestion; it does not implement physical clock gating.
- The supplied Vivado project and Tcl script use different FPGA part numbers. Match the target part before running the Tcl script.
- Report timing, area, power, and verification results only after checking actual Vivado reports and simulation results.

## Author

**Anuj Bansal**  
Electronics & Communication Engineering  
ABES Engineering College
