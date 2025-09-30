# Day 3: Combinational and Sequential Optimizations.

Welcome to **Day 3** of the RISC-V CHIP TAPEOUT PROGRAM Organized by VLSI System Design. Today we will Cover Topics related to Optimizations which include both Sequentail Logic Optimizations and Combinational Logic Optimizations. Let's dive deep into the topics.

## Contents:
1. [What is Logic Optimization.](#logic-optimiization)
2. [Types of Logic Optimizations.](#Types-of-logic-optimization)
3. [Labs on Sequential Logic Optimization.](#Sequential-logic-optimization)
4. [Labs on Combinational Logic Optimization.](#Combinational-logic-optimization)


# 1. [What is Logic Optimization.](#logic-optimiization)
❖ Logic optimization is the process of improving a digital circuit design to reduce area, delay, or power without changing its functionality.

❖ The goal is to achieve efficient, faster, and cost-effective hardware implementation.

# 2. [Types of Logic Optimization:](#Types-of-logic-optimization)

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

# 3. [Labs on Sequential Logic Optimization.](#Sequential-logic-optimization)

## Lab 1: 

Verilog Code

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/fb313ad826cf71d5a554982fb840d7f3d4e90034/Day3/dff_const1.v%20yosys%2028.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/fb313ad826cf71d5a554982fb840d7f3d4e90034/Day3/dff_const2%20yosys%2029.png)

## Lab 2:

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/3b54bebeada8c748cd42302ef3a3844fb085a154/Day3/dff_const3%20yosys.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/3b54bebeada8c748cd42302ef3a3844fb085a154/Day3/dff_const2.v%20gtkwave%2028.png)

## Lab 3:

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/f8ca84e0ba4d451a874312d18703224016f26e47/Day3/dff_const3.v%20gtkwave%2029%20full%20image.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/f8ca84e0ba4d451a874312d18703224016f26e47/Day3/dff_const3.v%20gtkwave%2029.png)

## Lab 4:

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/f8ca84e0ba4d451a874312d18703224016f26e47/Day3/dff_const4.v%20gtkwave%2029%20full%20image.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/f8ca84e0ba4d451a874312d18703224016f26e47/Day3/dff_const4%20yosys%20full%20image.png)

## Lab 5:

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/020a46e316ef0a16c80e0085d02dd243ab93855c/Day3/dff_const5.v%20gtkwave%2029%20full%20image.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/020a46e316ef0a16c80e0085d02dd243ab93855c/Day3/dff_const5.v%20gtkwave%2029.png)

# 4. [Labs on Combinational Logic Optimization.](#Combinational-logic-optimization)

## Lab 1:

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/6cd8d593dbb15d48dc8cc573bca4c861a6b612d9/Day3/DAY3%2027lab%20opt_check2.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/6cd8d593dbb15d48dc8cc573bca4c861a6b612d9/Day3/opt_check2.png)


![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/6cd8d593dbb15d48dc8cc573bca4c861a6b612d9/Day3/D1%20SK3%20L2%20Lab2.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/6cd8d593dbb15d48dc8cc573bca4c861a6b612d9/Day3/counter_opt2.v%20yosys%2031.png)



