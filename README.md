AXI-LiteBurst-32
A modular Verilog RTL project demonstrating an AXI4-Lite-style 32-bit memory-mapped slave interface, byte-strobe writes, response handling, and low-power idle monitoring. Developed for simulation and FPGA implementation using AMD/Xilinx Vivado.
Block Diagram
![AXI-LiteBurst-32 Block Diagram](images/axi_liteburst32_block_diagram.jpg)
Features
32-bit data path with parameterized 8-bit address width.
Five AXI4-Lite channels: AW, W, B, AR, and R.
Internal register memory of 16 × 32-bit words (64 bytes).
Byte-level write control using `WSTRB[3:0]`.
Read/write address decoding and response generation.
Low-power idle monitoring with activity detection and a `clock_enable` suggestion.
Separate burst-style address sequencer supporting 1–16 beats with 4-byte address increments.
RTL Overview
Module	Purpose
`axi_liteburst32_top.v`	Top-level slave integration
`axi_aw_channel.v`, `axi_w_channel.v`, `axi_b_channel.v`	Write channels
`axi_ar_channel.v`, `axi_r_channel.v`	Read channels
`address_decoder.v`	Address decoding
`write_data_path.v`, `read_data_path.v`	Write and read datapaths
`response_generator.v`	Read/write response generation
`low_power_controller.v`	Idle/activity monitoring
`burst_controller.v`	Standalone multi-transfer address sequencer
`axi_slave_fsm.v`, `reg_mem_bank.v`	Additional standalone modules
Design Specifications
Parameter	Value
HDL	Verilog
Top module	`axi_liteburst32_top`
Data width	32 bits
Address width	8 bits (parameterized)
Internal memory	16 × 32-bit words
Write strobes	4 bits
Reset	Active-low synchronous
Burst sequencer	1–16 beats, 4-byte increment
Simulation
Open `AXI_LiteBurst32.xpr` in Vivado.
Set `tb_axi_liteburst32_top` as the simulation top.
Select Run Simulation → Run Behavioral Simulation.
Check the simulation transcript and waveforms.
The project includes 14 Verilog testbenches. Run them in Vivado/XSim before reporting test results; successful execution has not been independently confirmed here.
Important Notes
AXI4-Lite does not support native burst transactions. `burst_controller.v` is a custom sequencer for successive single-beat transfers.
In the supplied RTL, `burst_controller.v`, `axi_slave_fsm.v`, and `reg_mem_bank.v` are standalone modules and are not instantiated in `axi_liteburst32_top.v`. The supplied diagram is included as the project's conceptual block diagram; check the RTL for the implemented top-level connectivity.
The low-power controller provides activity monitoring and a clock-enable suggestion; it does not implement physical clock gating.
The supplied `.xpr` targets `xc7z020clg400-1`, while `create_fresh_project.tcl` selects `xc7a35tcpg236-1`. Match the part to your FPGA board before using the Tcl script.
Do not claim measured timing, area, power, or successful verification without corresponding Vivado reports and simulation results.
Author
Anuj Bansal  
Electronics & Communication Engineering  
ABES Engineering College
