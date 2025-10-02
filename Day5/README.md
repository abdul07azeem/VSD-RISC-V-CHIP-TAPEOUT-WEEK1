# Day 5: Optimization in Synthesis


✨Welcome to the **final day of our learning journey!** Today, we will explore some of the most important **control flow statements in Verilog**—the building blocks that bring flexibility and decision-making into our designs. We will dive into **`if` statements** for conditional execution, **`case` statements** for multi-way branching, and different types of **looping constructs** (`for`) that help us efficiently implement repetitive operations in hardware. By mastering these, you’ll gain the ability to write **clean, optimized, and structured Verilog code** that not only simulates correctly but also synthesizes effectively. Let’s wrap up our session with a strong foundation in these essential programming constructs!

---
## **Contents**

1. **Introduction**
   * What is Optimzation in Synthesis and Importance.
2. **`if` Statement**

   * Definition
   * Syntax
  
3. **`case` Statement**

   * Definition
   * Syntax
  
4. **Looping Constructs**
    * Defintion.
    * Syntax
    * `for` Loop – Fixed iteration loops
    
5. **Labs**

---

Here’s a clear explanation of **optimization in synthesis** and its **importance**:

---

# **1. What is Optimization in Synthesis**

In digital design, **synthesis** converts RTL (Register Transfer Level) code into a **gate-level netlist** using logic gates and flip-flops.

**Optimization in synthesis** is the process of **improving the synthesized design** so that it meets specific goals—such as **speed, area, power, or reliability**—**without changing the circuit’s functionality**.

---

## **Importance of Optimization in Synthesis**

1. **Area Reduction**

   * Minimizes the number of gates, flip-flops, and interconnects.
   * Reduces silicon usage and manufacturing cost.

2. **Speed Improvement**

   * Ensures the design meets timing constraints (setup/hold times, max clock frequency).
   * Shortens critical paths and improves performance.

3. **Power Efficiency**

   * Reduces dynamic switching power and leakage current.
   * Important for battery-operated or low-power devices.
   * 

4. **Faster Simulation & Verification**

   * Smaller and simpler netlists speed up simulation and verification cycles.

# **2.'if' statement**


### **Definition**

The `if` statement is a **conditional branching construct** used to execute certain statements **only when a specified condition evaluates to true**. It allows decision-making in hardware designs.

---

### **Syntax**

```verilog
if (condition)
    statement1;
else if (condition2)
    statement2;
else
    statement3;
```

---

# 3. **`case` Statement**

### **Definition**

The `case` statement is a **multi-way branching construct** used to select and execute **one block of code** from several alternatives, based on the value of an expression. It is often used for **multiplexers, decoders, and finite state machines**.

---

### **Syntax**

```verilog
case (expression)
    value1 : statement1;
    value2 : statement2;
    ...
    default: statementN;
endcase
```
# **4. Looping Constructs**

Here’s a structured explanation for **Looping Constructs** in Verilog, starting with the general definition and the `for` loop:

---

# **Looping Constructs**

### **Definition**

Loops in Verilog are used to **repeat a block of statements multiple times**, reducing code redundancy and making designs more compact and readable. Loops are primarily used **inside procedural blocks** (`always` or `initial`) and are helpful in generating repeated hardware structures like counters, shift registers, or arrays of logic.

---

### **`for` Loop – Fixed Iteration Loops**

The `for` loop is used when the **number of iterations is known in advance**.

**Syntax:**

```verilog
for (initialization; condition; increment/decrement) begin
    // statements
end
```

**Example:**
<pre>
```verilog
integer i;
always @ (*)
 begin
    for (i = 0; i < 32; i = i + 1)
 begin
        if(i==sel)
          y = input[i];
    end
end
```</pre>

#### **NOTE: The Above verilog snippet with for loop is a much better method to write a Multiplexer compared to case Statement.**

# **Labs:**

**Lab 1:**

Verilog code

<pre>
module incomp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
always @ (*)
begin
        case(sel)
                2'b00 : y = i0;
                2'b01 : y = i1;
        endcase
end
endmodule
</pre>

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/7f57a88d1e1bf8bfa23bc4e78d520c7851052d1c/Day5/incomp_case.v%20day05%20gtkwave%2046.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/7f57a88d1e1bf8bfa23bc4e78d520c7851052d1c/Day5/incomp_if.v%20day%2005%20gtkwave%2044.png)

**Lab 2:**

Verilog code

<pre>
  module incomp_if (input i0 , input i1 , input i2 , output reg y);
always @ (*)
begin
        if(i0)
                y <= i1;
end
endmodule
</pre>

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/7f57a88d1e1bf8bfa23bc4e78d520c7851052d1c/Day5/incomp_if.v%20day05%20yosys%2044.png)

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/7f57a88d1e1bf8bfa23bc4e78d520c7851052d1c/Day5/incomp_if2.v%20day05%20%20gtkwave%2045.png)

**Lab 3:**

Verilog code

<pre>
  
module incomp_if2 (input i0 , input i1 , input i2 , input i3, output reg y);
always @ (*)
begin
        if(i0)
                y <= i1;
        else if (i2)
                y <= i3;

end
endmodule
                  
</pre>

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/7f57a88d1e1bf8bfa23bc4e78d520c7851052d1c/Day5/partial_case_assign%20.v%20day05%20yosys%2048.png)

**Lab 4:**

Verilog code

<pre>

module comp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
always @ (*)
begin
        case(sel)
                2'b00 : y = i0;
                2'b01 : y = i1;
                default : y = i2;
        endcase
end
endmodule
</pre>

**Lab 5:**

Verilog code

<pre>
module partial_case_assign (input i0 , input i1 , input i2 , input [1:0] sel, output reg y , output reg x);
always @ (*)
begin
        case(sel)
                2'b00 : begin
                        y = i0;
                        x = i2;
                        end
                2'b01 : y = i1;
                default : begin
                           x = i1;
                           y = i2;
                          end
        endcase
end
endmodule
</pre>


**Lab 6:**

<pre>
module bad_case (input i0 , input i1, input i2, input i3 , input [1:0] sel, output reg y);
always @(*)
begin
        case(sel)
                2'b00: y = i0;
                2'b01: y = i1;
                2'b10: y = i2;
                2'b1?: y = i3;
                //2'b11: y = i3;
        endcase
end
endmodule</pre>

**Lab 7:**

<pre>
module mux_generate (input i0 , input i1, input i2 , input i3 , input [1:0] sel  , output reg y);
wire [3:0] i_int;
assign i_int = {i3,i2,i1,i0};
integer k;
always @ (*)
begin
for(k = 0; k < 4; k=k+1) begin
        if(k == sel)
                y = i_int[k];
end
end
endmodule
</pre>

**Lab 8:**

<pre>
module demux_generate (output o0 , output o1, output o2 , output o3, output o4, output o5, output o6 , output o7 , input [2:0] sel  , input i);
reg [7:0]y_int;
assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;
integer k;
always @ (*)
begin
y_int = 8'b0;
for(k = 0; k < 8; k++) begin
        if(k == sel)
                y_int[k] = i;
end
end
endmodule
</pre>

**Lab 9:**

<pre>
module rca (input [7:0] num1 , input [7:0] num2 , output [8:0] sum);
wire [7:0] int_sum;
wire [7:0]int_co;

genvar i;
generate
        for (i = 1 ; i < 8; i=i+1) begin
                fa u_fa_1 (.a(num1[i]),.b(num2[i]),.c(int_co[i-1]),.co(int_co[i]),.sum(int_sum[i]));
        end

endgenerate
fa u_fa_0 (.a(num1[0]),.b(num2[0]),.c(1'b0),.co(int_co[0]),.sum(int_sum[0]));


assign sum[7:0] = int_sum;
assign sum[8] = int_co[7];
endmodule </pre>
