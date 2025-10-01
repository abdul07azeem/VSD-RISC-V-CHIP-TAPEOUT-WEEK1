# [Day 4: Gate Level Simulation, Blocking vs Non-Blocking Statements and Synthesis Simulation Mismatch.](Day4)

Welcome! In this session, we will explore the concept of **Gate Level Simulation(GLS)**, What are the major differences between **Blocking and Non-Blocking Statements**,How both types of Statements help in execution of logic,speed and efficiency of the design. Atlast we will Dive deep into labs relatd to 
**Synthesis-Simulation Mismatch.** 

---
## 📑 Table of Contents


1. **Gate Level Simulation (GLS)**
   
   * Definition and Purpose.
   * Importance of Gate Level Simulation (GLS).
   * Role of GLS in the design flow.

2. **Blocking vs Non-Blocking Statements**

   * Definition of Blocking Statements (`=`)
   * Definition of Non-Blocking Statements (`<=`)
   * How Blocking affects logic execution
   * How Non-Blocking improves speed & efficiency
    

3. **Synthesis-Simulation Mismatch**

   * What is a mismatch and why it happens
   * Common causes (e.g., improper use of blocking/non-blocking)
   * Consequences in real designs

4. **Lab Sessions:**

   * Lab 1: Gate Level Simulation Hands-On
   * Lab 2: Exploring Blocking vs Non-Blocking in simulation
   * Lab 3: Debugging Synthesis-Simulation Mismatch.
  
 # 1. **Gate Level Simulation (GLS)**

 **Gate Level Simulation (GLS)** is the process of simulating a digital design after synthesis, where the design is represented using logic gates and interconnections instead of high-level RTL code.
It verifies the correctness of the synthesized netlist against the intended functionality of the RTL.
GLS also helps detect **timing issues, glitches, and synthesis-simulation mismatches** that may not appear in RTL simulation.

### The **importance of Gate Level Simulation (GLS)** is:

1. **Verification after synthesis** – Ensures the synthesized netlist behaves the same as the RTL design.
2. **Catches synthesis-simulation mismatches** – Finds issues like incorrect optimizations, inferred latches, or wrong resets.
3. **Timing validation** – Helps check propagation delays, glitches, and race conditions that RTL simulation cannot show.
4. **Confidence before tapeout** – Provides an extra level of assurance that the fabricated chip will function correctly.

### The **role of Gate Level Simulation (GLS) in the design flow** is:

1. **Post-synthesis verification** – Confirms that the synthesized gate-level netlist matches the intended RTL functionality.
2. **Timing validation** – Checks timing with back-annotated delays (from SDF) to ensure setup/hold requirements are met.
3. **Glitch and race detection** – Identifies hazards, glitches, or X-propagation issues not visible in RTL simulation.
4. **Reset and power-up checks** – Ensures proper initialization of registers, especially in designs without explicit resets.
5. **Final sign-off check** – Acts as a safety net before place-and-route, giving confidence in correctness before moving to physical design.

**NOTE:  If the Gate Level models are delay annotated then we can use GLS for timing validation.**

# 2. Blocking vs Non-Blocking Statements:


### **1. Definition of Blocking Statements (`=`)**

* In Verilog, **blocking statements** execute **sequentially** (one after the other) within an **always block**.
* Syntax: `a = b;` → the assignment must complete before the next statement starts.

---

### **2. Definition of Non-Blocking Statements (`<=`)**

* **Non-blocking statements** allow all assignments to be evaluated first, and updates happen **in parallel** at the end of the time step.
* Syntax: `a <= b;` → scheduling updates without blocking the next statement.

---

### **3. How Blocking Affects Logic Execution**

* Works like normal programming assignment.
* Each statement **blocks** the execution of the next until it finishes.
* May cause **incorrect behavior in sequential circuits** (e.g., flip-flops) because the updated value is immediately visible within the same simulation cycle.

---

### **4. How Non-Blocking Improves Speed & Efficiency**

* All right-hand sides are evaluated first, then left-hand sides are updated **simultaneously**.
* Ideal for **clocked sequential logic**, ensuring registers capture correct values in the same clock cycle.
* Improves **simulation accuracy, speed, and efficiency**, avoiding race conditions and synthesis-simulation mismatches.


---

# 3. Synthesis-Simualtion Mismatch:


### **1. What is a Synthesis-Simulation Mismatch?**

* A **mismatch** occurs when the behavior of a design in **simulation** (RTL simulation) does **not match** the behavior of the synthesized netlist (after synthesis).
* This happens because synthesis tools and simulators may interpret certain coding styles differently.

---

### **Why does it happen?**

* RTL simulation assumes **ideal conditions** (zero delay, perfect resets, parallel updates).
* Synthesis maps the RTL code into **hardware gates/flip-flops**, where real timing, reset conditions, and logic optimizations apply.
* If coding is not done carefully, the simulator and synthesizer generate **different functional outcomes**.

---

### **2. Common Causes of Mismatch**

1. **Improper use of blocking (`=`) vs non-blocking (`<=`)**
   
   * Blocking in sequential logic may cause race conditions → simulation shows different results than synthesized hardware.
   
2. **Latch inference**
   
   * Forgetting to assign signals in all branches of an `always` block → simulator assumes “X”, but synthesis infers a latch.
   
3. **Uninitialized variables / reset issues**

   * RTL sim may start signals as `X`, but synthesis may optimize them differently.
 
4. **Asynchronous constructs not supported in hardware**
   
   * E.g., `#delay`, infinite loops, or `initial` blocks.
    
5. **Differences in optimization**
   
   * Synthesis might remove unused logic or optimize constants, while simulation still shows them.
  
6. **Missing Sensitivity List**

   * A Simulator evaluates output signal only when there is change in the state of input signal. If the always block is only sensitive to a single signal the
     simulator would not evaluate the output. So the best method is to write a always block for all the signals

     Ex: always @( sel)

     Simualtor would evaluate output only for the sel signal

     Best Approach:

     always@(*)

     the above statement would evaluate the code for all the changes occuring in all the signals of the circuit.

   

---

### **3. Consequences in Real Designs**

* **Functional bugs in silicon** – Design passes simulation but fails after fabrication.
* **Debugging complexity** – Hard to trace since simulation results looked “correct”.
* **Time & cost loss** – Wrong chips → costly re-spins and delays in tapeout.
* **Reduced reliability** – Undetected mismatches may cause random failures in real-world use.

---

# 4. Lab Sessions: 

## **Lab 1:**

Verilog Code:
<pre>
   module ternary_operator_mux(input i0 , input i1, input sel , output y);
assign y = sel?i1:i0;
endmodule
</pre>

<pre>
module ternary_operator_mux(i0, i1, sel, y);
  wire _0_;
  input i0;
  input i1;
  input sel;
  output y;
  assign _0_ = sel ? i1 : i0;
  assign y = _0_;
endmodule
</pre>

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/15b929a93844621baa9a84c203c9002406154e62/Day4/ternary_operator_mux.v%20Day04%20gls%20gtkwave.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/15b929a93844621baa9a84c203c9002406154e62/Day4/ternary_operator_mux.v%20gtkwave%20Day4%2037.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/15b929a93844621baa9a84c203c9002406154e62/Day4/ternary_operator_mux.v%20Day04%20yosys%2037.png)

## **Lab 2:**

<pre>

module bad_mux (input i0 , input i1 , input sel , output reg y);
always @ (sel)
begin
        if(sel)
                y <= i1;
        else
                y <= i0;
end
endmodule

</pre>

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/69414c55fba8037c545d4a317a70e59ab74ee544/Day4/bad_mux.v%20day04%2038%20yosys%20.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/69414c55fba8037c545d4a317a70e59ab74ee544/Day4/bad_mux.v%20day04%20gtkwave%2038.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/69414c55fba8037c545d4a317a70e59ab74ee544/Day4/blocking_caveat%20day04%20gtkwave%2039.png)

**Lab 3:**

Verilog code:
<pre>
   
module blocking_caveat (input a , input b , input  c, output reg d);
reg x;
always @ (*)
begin
        d = x & c;
        x = a | b;
end
endmodule

</pre>

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/69414c55fba8037c545d4a317a70e59ab74ee544/Day4/blocking_caveat.v%20day04%2040%20yosys.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/69414c55fba8037c545d4a317a70e59ab74ee544/Day4/blocking_caveat.v%20day04%20gtkwave%20gls.png)





  





