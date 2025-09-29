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

![](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/945f08ccc8526ff55f1646c9721522d217792948/Day2/multiple%20modules%201.png)

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

**NOTE:** The Asyncronous Flop doesnot wait for posedge pulse of the clock to work/execute.

## **Simulation Using iverilog and GTKWave:**

**Step 1: Compile**

<pre> iverilog dff_asyncres.v tb_dff_asyncres.v</pre>

**Step 2: Run** 

<pre> ./a.out </pre>

**Step 3: View Compiled Waveform**

<pre> gtkwave tb_dff_asyncres.vcd </pre>
   
![ ](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/8af83f2366034f933a58cdc0229e417685c4a5b1/Day2/dff_asyncres_day02_gtkwave%5B1%5D.png)

## **Synthesis using GTKWave:**

**Step 1:** Invoke Yosys

<pre>yosys</pre>

**Step 2:** Read the Liberty File

<pre>read_liberty -lib path/to/your/sky130_fd_sc_hd__tt__025C_1v80.lib</pre>

**Step 3:** Read Verilog Code

<pre>read_verilog /home/abdul/VLSI/sky130DesignAndSynthesisWorkshop/verilog_files/dff_asyncres.v</pre>

**Step 4:** Synthesize the design

<pre>synth -top dff_asyncres</pre>

**Step 5:** Technology Mapping

<pre>abc -liberty/address/to/your/sky130file/sky130_fd_sc_hd__tt__025C_1v80.lib</pre>

**Step 6:** Observe the Gate-level Netlist

<pre>show </pre>

![gtkwave tb_good_mux.vcd](https://github.com/abdul07azeem/VSD-RISC-V-CHIP-TAPEOUT-WEEK1/blob/8af83f2366034f933a58cdc0229e417685c4a5b1/Day2/dff_asyncres_day_02_yosys%5B1%5D.png)

---


# 🔑Key Takeaways

1. How Various Flip-Flop Coding Styles Actually work.
   
2. Key working Differences between Synchronous and Asyncronous Flipflops.

3. How unwanted waveform glitches can be eliminated using Flipflops.
   
4. Key Differences between Hierarchial and Flat Synthesis

5. Understood Importace and working of SKY130 Library.


















