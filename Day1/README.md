
# [Day 1: Introduction to Verilog RTL Design and Synthesis.](#Day1-Introduction-to-Verilog-RTL-Design-and-Synthesis.)

Welcome to **Day 1** of the RISC-V CHIP TAPEOUT PROGRAM! Today, we will explore the fundamentals of **digital design, simulation and synthesis** using open-source tools.  

Below is a structured overview of today's topics. These topics can help you build strong foundation as a beginner in RTL Design:

1. [What is Design, Testbench and How a Simulator Works](#how-a-simulator-works)  
2. [Introduction to iverilog and GTKWave](#designing-rtl-circuits)  
3. [Verilog Code Analysis](#testbenches-and-verification)  
4. [What are Libraries and Why there are Different Flavours of Gates](#getting-started-with-icarus-verilog-and-gtkwave)  
5. [Logic Synthesis with Yosys](#logic-synthesis-with-yosys)  

---
# 1. [What is Design, Testbench and How a Simulator Works?](#how-a-simulator-works)
## Design.

In VLSI **Design** refers to the process of defining the structure, behavior, and data flow of a digital system before it is implemented in hardware.

---

## TestBench

A testbench is a separate Verilog module used to verify the functionality of a design.
It applies inputs to the design and observes outputs over time.

---
## Simulator

Simulators are tools that imitate the behavior of hardware or software systems to verify their functionality without physically building them.

A Simulator looks for the changes on input signals.

If no changes to input signal then no change to output.

---
# 2. [Introduction to iverilog and GTKWave](#designing-rtl-circuits)
## Getting Started with Icarus Verilog and GTKWave

- **Icarus Verilog**: An open-source Verilog compiler and simulator. It compiles your design and testbench to generate simulation outputs.  
- **GTKWave**: A waveform viewer used to **visualize signal changes over time**.  
Together, these tools allow you to **simulate and debug** your digital designs efficiently.

**Commands to Install above tools:**

<pre>sudo apt install iverilog
sudo apt install gtkwave</pre>


---
# 3. [Verilog Code Analysis](#testbenches-and-verification)

# Lab: Simulating a 2:1 Multiplexer 
**Step 1:** Clone the Repositry

<pre>git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git

cd sky130RTLDesignAndSynthesisWorkshop/verilog_files</pre>


**Step 2:** Simulate Design using instructions below


<pre>iverilog good_mux.v tb_good_mux.v</pre>

**Step 3:** Execute the compiled simulation:
<pre>./a.out</pre>

**Step 4:** View Waveform in GTKWave using Value Change Dump file[vcd file]

<pre> gtkwave tb_good_mux.vcd file</pre>

![gtkwave tb_good_mux.vcd](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/3b3cdf4f7178037fade82084c8b7279920b6dc84/Day1/good_mux%20day01%20yosys.png)

The Code for the multiplexer is given as:


   <pre>module good_mux (input i0 , input i1 , input sel , output reg y);
   
	always @ (*)
	
	begin

		if(sel)
		
			y <= i1;
			
		else 
		
			y <= i0;
			
	end
	
	endmodule </pre>

		
  How it works:
  
 » The module has two inputs (i0, i1), one select line (sel), and one output (y).
 
 »  The always @(*) block makes it combinational logic (no clock needed).
 
 » If sel = 0, the output y takes the value of i0; if sel = 1, y takes the value of i1.
 
 » This implements a 2-to-1 multiplexer, choosing between two inputs based on the select signal.
	
---

# 4. [What are Libraries and Why there are Different Flavours of Gates](#getting-started-with-icarus-verilog-and-gtkwave)

In RTL design, **libraries** are collections of pre-characterized logic cells (like AND, OR, flip-flops, etc.) provided by the technology vendor.

They contain information about functionality, timing, power, and physical layout of each cell.

During synthesis, the tool maps your RTL code to these library cells to generate an optimized gate-level netlist.


**Standard cell libraries** provide predefined logic gates (AND, OR, XOR, etc.) and sequential elements (D flip-flops, latches) with known **timing and electrical characteristics**.  

Different **flavors of logic gates** exist to optimize for **speed, area, or power**. These libraries are used during synthesis to map RTL logic to **actual physical cells** in an ASIC.

---


# 5. [Logic Synthesis with Yosys](#logic-synthesis-with-yosys) 

## Logic Synthesis with Yosys

Let us now Synthesis good_mux file using Yosys

**Step 1:** Invoke Yosys

<pre>yosys</pre>

**Step 2:** Read the Liberty File

<pre>read_liberty -lib path/to/your/sky130_fd_sc_hd__tt__025C_1v80.lib</pre>

**Step 3:** Read Verilog Code

<pre>read_verilog /home/abdul/VLSI/sky130DesignAndSynthesisWorkshop/verilog_files/good|_mux.v</pre>

**Step 4:** Synthesize the design

<pre>synth -top good_mux</pre>

**Step 5:** Technology Mapping

<pre>abc -liberty/address/to/your/sky130file/sky130_fd_sc_hd__tt__025C_1v80.lib</pre>

**Step 6:** Observe the Gate-level Netlist

<pre>show </pre>

![gtkwave tb_good_mux.vcd](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/3b3cdf4f7178037fade82084c8b7279920b6dc84/Day1/good_mux.v.png)

---
## Summary
 »  Learned and understood Simulators, Testbenches, Designs.
 
 » Importance of Various Gate Flavours, libraries.
 
 » Learned tools such as iverilog, gtkwave and yosys.


