# Day 3: Combinational and Sequential Optimizations.

Welcome to **Day 3** of the RISC-V CHIP TAPEOUT PROGRAM Organized by VLSI System Design. Today we will Cover Topics related to Optimizations which include both Sequentail Logic Optimizations and Combinational Logic Optimizations. Let's dive deep into the topics.

## Contents:
1. [What are Asynchronous and Synchronous D Flip-Flops.](#d-flipflops)
2. [What is Logic Optimization.](#logic-optimiization)
3. [Types of Logic Optimizations.](#Types-of-logic-optimization)
4. [Labs on Sequential Logic Optimization.](#Sequential-logic-optimization)
5. [Labs on Combinational Logic Optimization.](#Combinational-logic-optimization)

# 1. [What are Asynchronous and Synchronous D Flip-Flops.](#d-flipflops)

### **Synchronous D Flip-Flop**

* A **synchronous D flip-flop** changes its output **only on the triggering edge of the clock** (positive or negative edge).
* Any input like **reset** or **set** works only when the **clock edge arrives**.
* Example: If `D=1` at the rising clock edge, output `Q` becomes `1`.

---

### **Asynchronous D Flip-Flop**

* An **asynchronous D flip-flop** has **direct set/reset inputs** that affect the output **immediately**, regardless of the clock.
* These asynchronous inputs **override the clock and D input** when activated.
* Example: If `RESET=1`, output `Q` is forced to `0` instantly, even if no clock edge occurs.

---

# 2. [What is Logic Optimization.](#logic-optimiization)
❖ Logic optimization is the process of improving a digital circuit design to reduce area, delay, or power without changing its functionality.

❖ The goal is to achieve efficient, faster, and cost-effective hardware implementation.

# 3. [Types of Logic Optimization:](#Types-of-logic-optimization)

## Sequential Logic Optimization:

**Sequential logic optimization** is the process of improving the efficiency of circuits that include memory elements (like flip-flops and latches) while preserving their functional behavior over time.

❖ It focuses on optimizing **register placement, retiming, state encoding, and clocking** to reduce area, power, or timing delays.

## 1. Sequential Constant:

**Sequential constant optimization** is an optimization technique applied to **sequential circuits** (those with flip-flops, latches, or state machines), where registers or states that hold a constant value across all clock cycles are identified and replaced with that constant.

* If a flip-flop always stores `0` or `1`, it is redundant and can be removed.

✅ Example:
If a D flip-flop’s input is always tied to `1`, then its output `Q` will always be `1` after the first clock — the flip-flop can be replaced with a constant logic `1`.

## 2. State Optimization of Unused States:

**State optimization of unused states** means assigning or reusing the **unused/unreachable states** in a finite state machine (FSM) in such a way that they do not increase hardware complexity.

* If certain state codes (due to binary encoding of flip-flops) are **never reached in normal operation**, they are treated as **don’t care conditions** during synthesis.
* Optimizing these unused states helps minimize the next-state logic and prevents unexpected behavior if the FSM accidentally enters an unused state.

## 3. Cloning:

In digital design, **cloning** is a **logic optimization technique** where a logic gate or a sequential element (like a flip-flop) is **duplicated** to reduce long fanout or large delay.

By cloning, the load is split between the copies, which helps **improve timing, reduce delay, and balance the design**, without changing functionality.


## Combinational Logic Optimization:


## **1. Constant Propagation:**

**Constant propagation** is an optimization technique where constant values in a circuit or program are identified and directly substituted into the logic.

✅ Example:

A AND gate having inputs A and B and output D. The D output is fed to a NOR gate along with another input C producing a output Y. The Complete logic can be described as:  
      **Y = ((A.B)+C)'**

Assume the value of input A is zero for all the operations. 

In this type of synthesis the tool Optimizies the circuit from a Combination of AND gate and NOR gate to a single NOT gate or a Inverter. 

This type of Optimization is called as **Constant Propagation.**

# 4. [Labs on Sequential Logic Optimization.](#Sequential-logic-optimization)

## Simulation and Synthesis Flow:

**1. Icarus Verilog:**
<pre> 
     Step 1: Compile the verilog Code:
     iverilog design_file.v testbench_file.v

     Step 2: Generate Value Change Dump File
      ./a.out

     Step 3: View Waveform in GTKWave
     gtkwave vcdfile.vcd
</pre>

**2. Synthesis and Optimization in Yosys**

<pre>
Step 1: Invoke yosys
     yosys
     
Step 2:Read Liberty file
</pre>

## Lab 1: 

Verilog Code

<pre>module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
        if(reset)
                q <= 1'b0;
        else
                q <= 1'b1;
end
endmodule </pre>

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/fb313ad826cf71d5a554982fb840d7f3d4e90034/Day3/dff_const1.v%20yosys%2028.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/fb313ad826cf71d5a554982fb840d7f3d4e90034/Day3/dff_const2%20yosys%2029.png)

## Lab 2:

Verilog code

<pre>module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
        if(reset)
                q <= 1'b1;
        else
                q <= 1'b1;
end
endmodule</pre>

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/3b54bebeada8c748cd42302ef3a3844fb085a154/Day3/dff_const3%20yosys.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/3b54bebeada8c748cd42302ef3a3844fb085a154/Day3/dff_const2.v%20gtkwave%2028.png)

## Lab 3:

Verilog Code
<pre>module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
        if(reset)
        begin
                q <= 1'b1;
                q1 <= 1'b0;
        end
endmodule</pre>

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/f8ca84e0ba4d451a874312d18703224016f26e47/Day3/dff_const3.v%20gtkwave%2029%20full%20image.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/f8ca84e0ba4d451a874312d18703224016f26e47/Day3/dff_const3.v%20gtkwave%2029.png)

## Lab 4:

Verilog Code

<pre>module dff_const4(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
        if(reset)
        begin
                q <= 1'b1;
                q1 <= 1'b1;
        end
        else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end 
endmodule</pre>

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/f8ca84e0ba4d451a874312d18703224016f26e47/Day3/dff_const4.v%20gtkwave%2029%20full%20image.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/f8ca84e0ba4d451a874312d18703224016f26e47/Day3/dff_const4%20yosys%20full%20image.png)

## Lab 5:

Verilog Code

<pre>module dff_const5(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
        if(reset)
        begin
                q <= 1'b0;
                q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end
endmodule</pre>

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/020a46e316ef0a16c80e0085d02dd243ab93855c/Day3/dff_const5.v%20gtkwave%2029%20full%20image.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/020a46e316ef0a16c80e0085d02dd243ab93855c/Day3/dff_const5.v%20gtkwave%2029.png)

# 5. [Labs on Combinational Logic Optimization.](#Combinational-logic-optimization)

## Lab 1:



![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/6cd8d593dbb15d48dc8cc573bca4c861a6b612d9/Day3/DAY3%2027lab%20opt_check2.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/6cd8d593dbb15d48dc8cc573bca4c861a6b612d9/Day3/opt_check2.png)


![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/6cd8d593dbb15d48dc8cc573bca4c861a6b612d9/Day3/D1%20SK3%20L2%20Lab2.png)





