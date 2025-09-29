
# Day 1: Introduction to Verilog RTL Design and Synthesis.

Welcome to **Day 1** of the RISC-V CHIP TAPEOUT PROGRAM! Today, we will explore the fundamentals of **digital design, simulation and synthesis** using open-source tools.  

Below is a structured overview of today's topics. These topics can help you build strong foundation as a beginner in RTL Design:

1. [What is Design, Testbench and How a Simulator Works](#how-a-simulator-works)  
2. [Introduction to iverilog and GTKWave](#designing-rtl-circuits)  
3. [Verilog Code Analysis](#testbenches-and-verification)  
4. [Why Different Flavours of Gates](#getting-started-with-icarus-verilog-and-gtkwave)  
5. [Logic Synthesis with Yosys](#logic-synthesis-with-yosys)  

---

## Design(#how-a-simulator-works)(#how-a-simulator-works)

In VLSI **Design** refers to the process of defining the structure, behavior, and data flow of a digital system before it is implemented in hardware.

---

## TestBench

A testbench is a separate Verilog module used to verify the functionality of a design.
It applies inputs to the design and observes outputs over time.

---
## Simulator

A testbench is a separate Verilog module used to verify the functionality of a design.
It applies inputs to the design and observes outputs over time.

---

## Getting Started with Icarus Verilog and GTKWave(#designing-rtl-circuits) 

- **Icarus Verilog**: An open-source Verilog compiler and simulator. It compiles your design and testbench to generate simulation outputs.  
- **GTKWave**: A waveform viewer used to **visualize signal changes over time**.  
Together, these tools allow you to **simulate and debug** your digital designs efficiently.

---
## Verilog Code Analysis(#testbenches-and-verification) 

# Lab: Simulating a 2:1 Multiplexer 
Step 1: Clone the Repositry
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files

Step 2: Install Required Tools Such as iverilog and GTKWave
sudo apt install iverilog
sudo apt install gtkwave

Step 3: Simulate Design using instructions below

iverilog good_mux.v tb_good_mux.v

Run the simulation:
./a.out

View Waveform in GTKWave using Value Change Dump file[vcd file]

![gtkwave tb_good_mux.vcd](D:\Day1\good_mux.png)

The Code for the multiplexer is given below as:

	module good_mux (input i0 , input i1 , input sel , output reg y);
	always @ (*)
	begin
		if(sel)
			y <= i1;
		else 
			y <= i0;
	end
	endmodule

  How it works:
 » The module has two inputs (i0, i1), one select line (sel), and one output (y).
 »  The always @(*) block makes it combinational logic (no clock needed).
 » If sel = 0, the output y takes the value of i0; if sel = 1, y takes the value of i1.
 » This implements a 2-to-1 multiplexer, choosing between two inputs based on the select signal.
	
---

## Why Different Flavours of Gates(#getting-started-with-icarus-verilog-and-gtkwave)  

**Standard cell libraries** provide predefined logic gates (AND, OR, XOR, etc.) and sequential elements (D flip-flops, latches) with known **timing and electrical characteristics**.  
Different **flavors of logic gates** exist to optimize for **speed, area, or power**. These libraries are used during synthesis to map RTL logic to **actual physical cells** in an ASIC.

---


## Logic Synthesis with Yosys(#logic-synthesis-with-yosys)

Let us now Synthesis good_mux file usinf Yosys
**Step 1** Invoke Yosys
yosys
**Step 2**
read_liberty -lib path/to/your/sky130_fd_sc_hd__tt__025C_1v80.lib
**Step 3**
read_verilog /home/abdul/VLSI/sky130DesignAndSynthesisWorkshop/verilog_files/good|_mux.v
**Step 4** Synthesize the design
synth -top good_mux
**Step 5** Technology Mapping
abc -liberty/address/to/your/sky130file/sky130_fd_sc_hd__tt__025C_1v80.lib
**Step 6** Observe the Gate-level Netlist
show 

![gtkwave tb_good_mux.vcd](D:\Day1\good_mux.v yosys.png)

---
## Summary
 »  Learned and understood Simulators, Testbenches, Designs
 » Importance of Various Gate Flavours
 » Learned tools such as iverilog, gtkwave and yosys


