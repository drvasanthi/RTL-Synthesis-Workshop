<h1 align="center">SKY130 - RTL-Synthesis-Workshop</h1>

## TABLE OF CONTENTS

1. [**Day 1**:  Introduction to Verilog RTL Design and Synthesis](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop/blob/main/README.md#1-introduction-to-verilog-rtl-design-and-synthesis)
	1. [SKY130 RTL Introduction to Open-source Iverilog Simulator ](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#11-SKY130-rtl-introduction-to-open-source-iverilog-simulator)
		1. [Design](https://github.com/drvasanthi/RTL-Design-and-Synthesis#i--iverilog)
		2. [Testbench](https://github.com/drvasanthi/RTL-Design-and-Synthesis#ii-gtkwave)
		3. [Simulator](https://github.com/drvasanthi/RTL-Design-and-Synthesis#iii--yosys)
	2. [SKY130 RTL Introduction to Yosys and Logic Synthesis ](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#11-SKY130-rtl-introduction-to-open-source-iverilog-simulator)

2. [**Day 2**: Introduction to .lib, Heirarchial vs flat synthesis and Flop coding style](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#2-introduction-to-lib-heirarchial-vs-flat-synthesis-and-flop-coding-style)
    1. [Introduction to .lib](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#21-introduction-to-lib)
    2. [Heirarchial vs flat synthesis](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#22-heirarchial-vs-flat-synthesis)
    3. [ Flop coding style](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#23-flop-coding-style)
    	1. [Flop with asynchronous set/reset](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#flop-with-asynchronous-setreset)
    	2. [Flop with synchronous set/reset](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#flop-with-synchronous-setreset)
    	3. [Flop with asynchronous and synchronous set/reset](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#flop-with-synchronous-and-asynchronous-setreset)
    	
3. [**Day 3**:  Introduction to optimisation](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#3-introduction-to-optimisation)
	1. [Optimization of combinational circuits](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#31-optimization-of-combinational-circuits)
		1. [Constant propagation](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#constant-propagation)
		2. [Optimization of boolean logic](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#optimization-of-boolean-logic)
	2.  [Optimization of sequential circuits](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#32-optimization-of-sequential-circuits)
		1. [Optimization Sequential circuit using constant propagation](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#optimization-sequential-circuit-using-constant-propagation)\

4. [**Day 4**: GLS, blocking v/s non-blocking, and synthesis-simulation mismatch](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#41-gls---gate-level-simulation)
	1. [4.1 GLS - Gate Level Simulation ](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#41-gls---gate-level-simulation)
	2. [4.2 Synthesis Simulation Mismatch](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#42-synthesis-simulation-mismatch)

5. [**Day 5**: If Case Statements and for loop & for generate statements](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#5-if-case-statements-and-for-loop--for-generate-statements)
	1. [IF statements](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#51-if-statement) 
	2. [CASE statements](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#52-case-statement)
	3. [looping constructs](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#53-looping-constructs)

[**Acknowledgement**](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/README.md#acknowledgement)


## **1. Introduction to Verilog RTL Design and Synthesis**

Register Transfer Logic (RTL) is used to capture logic in design phase of the integrated circuit design cycle. A logic synthesis tool converts an RTL description written in Hardware Description Language (Verilog/VHDL) to a gate-level description of the circuit. Placement and routing tools use the synthesis outputs to generate a physical layout. The following figure shows the flow of RTL synthesis.

### **i. SKY130 RTL Introduction to Open-source Iverilog Simulator**   
Icarus Verilog(iverilog) is a Verilog simulator used to verify functional description of a design. It functions as a compiler, converting Verilog source code into a target format. VCD (Value Change Dump) is a standard dump format for Verilog that dumps the status of the design as it simulates. The iverilog simulator takes a verilog design file and its test bench as inputs. The following figure illustrates the inputs and outputs of iverilog simulator.
![image](https://user-images.githubusercontent.com/67214592/183249132-c009f5ee-4e72-48af-b6c3-8b6ec0cfcbec.png)
#### **a. Design**  
* Design is the actual verilog code or set of verilog codes, which has the intended functionality to meet with the required specifications. 
#### **b. Testbecnh**
* Testbench is the setup to apply stimulus (test_vector) to the design to check its functionality.
#### **c. Simulator**
* RTL design is checked for adhere to the spec by simulating the design.  
* Iverilog simulator is the tool used for simulating the design.  
* Simulator looks for the changes on input signal.
* Upon every changes in input, the output is evaluated. 
![image](https://user-images.githubusercontent.com/67214592/183249220-b1a3dd1d-743e-4b75-bb23-4f24bb77a3ef.png)
* Design will be instantiated in the testbench, then their will be a mechanism to apply the stimulus to the design.
* GTKWave is a VCD waveform viewer based on the GTK library. This viewer support VCD and LXT formats for signal dumps.  

### **ii. SKY130 RTL Introduction to Yosys and Logic Synthesis**  
Yosys is an open source RTL synthesis tool which takes verilog file of a design and technology library file(.lib) as inputs and generates gate level netlist corresponding the functional behaviour of the design.  
* Yosys Synthesizer tool used for converting the RTL to Netlist.
* Netlist is the representation of the design in form of the standard cell in `.lib`.

![image](https://user-images.githubusercontent.com/67214592/183249785-18fb67ab-f770-4390-88ea-a0cd0de73ad9.png)

To Verify the Synthesis:  
  *The testbench used in synthesis should be same as the RTL testbech. The output of the gtkwave should be same as output observed during RTL simulation.*

![image](https://user-images.githubusercontent.com/67214592/183249738-8b4011cc-cb80-4751-ac1c-203e06a18a82.png)

#### **Logic Synthesis**

![image](https://user-images.githubusercontent.com/67214592/183250146-702c3093-add2-48ca-87b4-65dd08282aa7.png)

1. RTL Design  
* It is the behavioral representation of the required specification.  
2. .lib  
* It has collection of logical modules.  
* It also includes basic logic gtes like AND, OR, NOT etc.,  
* Contains information about standard cell such area, power and timing, characterised for different PVT conditions.
* Guide the synthesizer to select the flavoured of gate cells like `slow cell`, `medium cell`, `fast cell`, for optimum implementation of logic circuits.  
3. Synthesis
* Synthesis is the RTL to gate level translation.  
* The design is converted into gates and the connections are made between the gates.  
* This is given out as a file called Netlist.  

### Table 1.1 : List of commands used in RTL Simultion  
|**Commands**|**Description**|
| :-: | :-: |
|  `iverilog verilogfilename.v tb_verilogfilename.v` |<p>To compile verilog design file and testbench file .</p><p>Ex: iverilog and21.v tb\_and21.v</p>|
|  `./a.out`|To generate VCD file|
|  `gtkwave tb_verilogfilename.vcd` |To invoke the waveform|

### Table 1.2 : List of commands used in Synthesis  
|**Commands**|**Description**|
| :-: | :-: |
|`Yosys`|To invoke open source logic synthesizer|
|`read_liberty -lib ../my_lib/lib/sy130_fd_sc_hd__tt_025C_1V80.lib`|To read .lib file |
|`read_verilog verilogfilename.v`|To read verilog design file|
|`synth -top verilogfilename`|To synthesize by setting a design as a top modules, if there are one or more submodules.|
|`abc -liberty ../my_lib/lib/sy130_fd_sc_hd__tt_025C_1V80.lib`|To generate gate level netlist|
|`write_verilog -noattr  verilogfilename_netlist.v`|To write netlist into a verilog file.|
|`show`|To display gate level schematic of the design|




