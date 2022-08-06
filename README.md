<h1 align="center">SKY130 - RTL-Synthesis-Workshop</h1>

## TABLE OF CONTENTS

1. [**Day 1**:  Introduction to Verilog RTL Design and Synthesis](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop/blob/main/README.md#1-introduction-to-verilog-rtl-design-and-synthesis)
	1. [SKY130 RTL Introduction to Open-source Iverilog Simulator ](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#11-SKY130-rtl-introduction-to-open-source-iverilog-simulator)
		1. [Simulator](https://github.com/drvasanthi/RTL-Design-and-Synthesis#i--iverilog)
		2. [Design](https://github.com/drvasanthi/RTL-Design-and-Synthesis#ii-gtkwave)
		3. [Testbench](https://github.com/drvasanthi/RTL-Design-and-Synthesis#iii--yosys)
		4. [How Simulator Works](https://github.com/drvasanthi)
		5. [Simulation Flow of Iverilog](https://github.com/drvasanthi) 
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
		1. [Optimization Sequential circuit using constant propagation](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#optimization-sequential-circuit-using-constant-propagation)
4. [**Day 4**: GLS, blocking v/s non-blocking, and synthesis-simulation mismatch](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#41-gls---gate-level-simulation)
	1. [4.1 GLS - Gate Level Simulation ](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#41-gls---gate-level-simulation)
	2. [4.2 Synthesis Simulation Mismatch](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#42-synthesis-simulation-mismatch)
5. [**Day 5**: If Case Statements and for loop & for generate statements](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#5-if-case-statements-and-for-loop--for-generate-statements)
	1. [IF statements](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#51-if-statement) 
	2. [CASE statements](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#52-case-statement)
	3. [looping constructs](https://github.com/mrshashi4u/RTL-Design-and-Synthesis#53-looping-constructs)
6. [**Acknowledgement**](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/README.md#acknowledgement)


## **1. Introduction to Verilog RTL Design and Synthesis**

Register Transfer Logic (RTL) is used to capture logic in design phase of the integrated circuit design cycle. A logic synthesis tool converts an RTL description written in Hardware Description Language (Verilog/VHDL) to a gate-level description of the circuit. Placement and routing tools use the synthesis outputs to generate a physical layout. The following figure shows the flow of RTL synthesis.

{: .alert .alert-info .text-justify}

![image](https://user-images.githubusercontent.com/67214592/183248599-fe5ac867-002b-479f-8729-0e6dd5ecbd36.png)



