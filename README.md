# MIPS Multicycle Processor (SystemVerilog)

The microprocessor at the heart of any computer system. Here, I implement a
multicycle processor supporting a significant subset of the MIPS
instruction set architecture. All instructions and dependencies were fully tested using various testbenches.


### Specification

</div>

My multicycle processor supports the following MIPS
instructions:

| R-types | I-types | J-types |
| :------ | :------ | :------ |
| `and`   | `andi`  | `j`     |
| `or`    | `ori`   | `jal`   |
| `xor`   | `xori`  | `jr`    |
| `nor`   | `slti`  |         |
| `sll`   | `addi`  |         |
| `srl`   | `beq`   |         |
| `sra`   | `bne`   |         |
| `slt`   | `lw`    |         |
| `add`   | `sw`    |         |
| `sub`   |         |         |
| `nop`   |         |         |

<div id="simulation">
### This repo contains the following:
    
  - SystemVerilog files

  - synthesized bitstream

  - A post-route utilization report

  - The provided constraint file

  - The provided Tcl scripts

  - Datapath schematic

  - FSM diagram (high-level)

  - Assembly test (`test.asm`)

  - Testing methodology description
 


#### Arithmetic Logic Unit (ALU)

</div>

> A provided ALU is defined in `alu.sv` and supports a zero flag as well as the operations listed below (opcode `` `defines `` shown in parentheses are included in `cpu.svh`).

  - and (`ALU_AND`)

  - or (`ALU_OR`)

  - xor (`ALU_XOR`)

  - nor (`ALU_NOR`)

  - signed addition (`ALU_ADD`)

  - signed subtraction (`ALU_SUB`)

  - signed “set less than” (`ALU_SLT`)

  - shift right logical (`ALU_SRL`)

  - shift left logical (`ALU_SLL`)

  - shift right arithmetic (`ALU_SRA`)

<div id="register-file">

#### Register file

</div>

> A provided register file is defined in `reg_file.sv` and supports two
read ports and one write port.

It also supports one additional “debug” read port for displaying the
contents of a register when running on the FPGA. (During simulation this
port can be ignored.) The register file is parameterized, but by default
it is specified to be \(32\times32\) (the size of a standard 32-bit MIPS
processor register file).

<div id="control">

### Control

</div>

The control unit generates the select and control signals that govern
*how* the datapath performs its computation for a given instruction.
Since the processor is multicycle, as the instruction advances through
the stages of the datapath, the control unit must continuously update
the control signalsṄote that multiple stages in your datapath may be put
to use simultaneously. Since the control
signals must update over time, we implement the control unit as an FSM.


<div id="clock-divider">

### Clock divider

</div>

> A provided clock divider is defined in `clk\_divider.sv`.

To maintain the synchronous nature of the design, the processor accepts a high-speed clock (`clk_100M`) **and**
divided version (`clk_en`). When using flip flops in your design, the
high-speed clock should be used as the clock input, and the divided
clock should be used as the enable. This ensures that our flip flops are
fully synchronous but will only operate at the divided clock speed. If
we connected the divided clock directly to the clock input of the flip
flop, this may result in additional clock skew. In general, one single
clock should be used for all flip flops.




<br> <br>

