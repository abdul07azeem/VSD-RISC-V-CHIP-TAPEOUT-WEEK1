# Day 2: Timing libraries, Hierarchial vs Flat Synthesis and efficient Coding Styles.

Welcome to **Day 2** of the RISC-V CHIP TAPEOUT PROGRAM! Today we will dive deep into topics like timing libraries, What are the Differences betweeen Hierarchial Synthesis and Flat Synthesis and what are the various coding styles which we can use to write a verilog code.

# Contents

1. [Introduction to Timing Libraries.](#timing-libraries)
2. [Hierarchial Synthesis vs Flat Synthesis.](#synthesis.)
3. [Why Flops and Flop coding Styles.](#flops)

# 1. [Introduction to Timing Libraries.](#timing-libraries)

➼ In RTL design, **timing libraries** (often in `.lib` format) are files that describe the timing, power,temperature and functional characteristics of standard cells in a technology.

➼ They specify details like propagation delay, setup/hold times, transition times, and power consumption under different conditions.

➼ Synthesis and STA (Static Timing Analysis) tools use timing libraries to ensure the RTL design meets performance requirements at the chosen process, voltage, and temperature (PVT) corners.

---

### SKY130 Standard Cell Library – `sky130_fd_sc_hd__tt_025C_1v80`

The file **`sky130_fd_sc_hd__tt_025C_1v80.lib`** is a **timing library** from the **SkyWater SKY130 PDK**, belonging to the **High-Density (HD) standard cell family**.
It provides characterized timing, power, and functional data for the following conditions:

* **Process Corner**: `tt` → *Typical-Typical* (both NMOS and PMOS devices modeled under typical process variation).
* **Temperature**: `025C` → *25 °C*, representing standard operating temperature.
* **Voltage**: `1v80` → *1.80 V nominal supply voltage*.

➼ **Impact of Size:**

Large Cell ➼ More Area ➼ Faster Execution ➼ High Power Consumption.

Small Cell ➼ Less Area ➼ Slower Execution ➼ Less Power Consumption.

**Exploring the .lib File**

1. **Install a text editor**
<pre>sudo apt update
sudo apt install vim -y </pre>

2. **Open SKY130 Library**
<pre> vim sky130_fd_sc_hd__tt_025C_1v80 </pre>


   # add image
   
---

# 2. [Hierarchial Synthesis vs Flat Synthesis.](#synthesis.)


| Aspect                   | **Hierarchical Synthesis**                                                      | **Flat Synthesis**                                                             |
| ------------------------ | ------------------------------------------------------------------------------- | -------------------------------------------------------------------------------|
| **Definition**           | Maintains the design hierarchy (modules/submodules preserved) during synthesis. | Flattens the design into a single-level netlist, ignoring module hierarchy. |
| **Design Readability**   | Easy to understand and debug since hierarchy is preserved.                      | Harder to trace back to original RTL as module boundaries are lost.       |
| **Runtime & Memory**     | Faster synthesis and uses less memory (smaller problem space per module).       | Slower and memory-intensive for large designs (entire design optimized at once). |
| **Optimization Quality** | Limited optimization across module boundaries.                                  | Better global optimization across the entire design.                    |
| **Reuse**                | Encourages IP/block reuse (modules can be synthesized independently).           | No reuse, every build starts from scratch.                                     |

---

# **Hierarchical Synthesis**

## **✅Advantages:**

* Easier debugging and ECO (Engineering Change Order).
* Promotes modular design and IP reuse.
* Shorter synthesis runtime for large projects.

 ## **❌Disadvantages:**
* Suboptimal QoR (Quality of Results) since optimizations stop at module boundaries.
* Interconnect delays between modules may hurt timing.

# **Flat Synthesis**

## **✅Advantages:**

* Better QoR (timing, area, power) due to global optimization.
* Eliminates unnecessary module boundaries and buffers.

## **❌Disadvantages:**
*  Long runtime and very high memory usage.
*  Debugging is harder (original hierarchy is lost).
*  Poor scalability for very large designs.

---

## 🔑 Important Point:

➡ In **industrial SoCs**, designers often use a **hybrid approach**: hierarchical synthesis for top-level + flat synthesis for critical blocks.


---

# 3. [Why Flops and Flop coding Styles.](#flops)

**Definition of a Flip-Flop:**

A **flip-flop** is a digital memory element that stores one bit of data and changes its output only on a triggering clock edge.

Below are various flip-flop coding styles:

## Asynchronous Reset D Flip-Flop
<pre>module dff_asyncres ( input clk ,  input async_reset , input d , output reg q );
always @ (posedge clk , posedge async_reset)
begin
        if(async_reset)
                q <= 1'b0;
        else
                q <= d;
end
endmodule</pre>

















