<h1 align="center">SKY130 RTL Design and Synthesis using IVerilog</h1>

## TABLE OF CONTENT

1. [**Day 1**:  Introduction to Verilog RTL Design and Synthesis](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop/blob/main/README.md#1-introduction-to-verilog-rtl-design-and-synthesis)
	1. [SKY130 RTL Introduction to Open-source Iverilog Simulator ](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#11-SKY130-rtl-introduction-to-open-source-iverilog-simulator)
		1. [Design](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#i--design)
		2. [Testbench](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#ii-testbench)
		3. [Simulator](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#iii--simulator)
	2. [SKY130 RTL Introduction to Yosys and Logic Synthesis ](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#11-SKY130-rtl-introduction-to-open-source-iverilog-simulator)

2. [**Day 2**: Introduction to timing libs, heirarchial vs flat synthesis and efficient flop coding style](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#2-introduction-to-timing-lib-heirarchial-vs-flat-synthesis-and-efficient-flop-coding-style)
    1. [Introduction to timing.libs](https://github.com/drvasnthi/SKY130-RTL-Synthesis-Workshop#21-introduction-to-lib)
    2. [Heirarchial vs flat synthesis](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#22-heirarchial-vs-flat-synthesis)
    3. [ Various Flop Coding Styles and Optimization](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#23-flop-coding-style)
    	1. [Flop with asynchronous set/reset](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#flop-with-asynchronous-setreset)
    	2. [Flop with synchronous set/reset](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#flop-with-synchronous-setreset)
    	3. [Flop with asynchronous and synchronous set/reset](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#flop-with-synchronous-and-asynchronous-setreset)
    	4. [Optimization](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#optimization) 
    	
3. [**Day 3**:  Combinational and Sequential Optimization](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#3-combinational-and-sequential-optimization)
	1. [Combinational Logic Optimization](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#31-optimization-of-combinational-circuits)
		1. [Constant propagation](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#constant-propagation)
		2. [Boolean logic optimization](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#optimization-of-boolean-logic)
	2.  [Sequential Logic Optimization](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#32-optimization-of-sequential-circuits)
		1. [Optimization Sequential circuit using constant propagation](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#optimization-sequential-circuit-using-constant-propagation)\

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

## **2. Introduction to timing libs, heirarchial vs flat synthesis and efficient flop coding styles**

### **i. Introduction to timing.libs**
 
***.lib*** stands for Liberty Timing File. 
The .lib file is an ASCII representation of the timing and power parameters associated with any cell in a particular semiconductor technology.It consists of timing and power parameters are obtained by simulating the cells under a variety of conditions (PVT) and the data is represented in the .lib format
The .lib file contains timing models and data to calculate
- I/O delay paths
- Timing check values
- Interconnect delays

We use an open source .lib file from Google Skywater sky130_fd_sc_hd__tt_025C_1v80.lib.
![image](https://user-images.githubusercontent.com/67214592/183252687-ce9eb8b9-5cd0-47f6-879d-2511b13dd2e7.png)

The naming convention is as follows

|**abbrevation**|**Description**|
| :-: | :-: |
|sky130|Represents technology node 130nm|
|fd|Foundary Dependent|
|sc|Standard cell|
|hd|High Desnsity|
|tt|Typical Process Corner|
|025|25c Temperature|
|1v80|1.8V|

![image](https://user-images.githubusercontent.com/67214592/183252705-f56fc741-a9e1-4e9d-87f8-fd3326f6fcd7.png)

The above clip from .lib files shows the information of Timing, power area and other details of standard cell AND gate.

### **ii. Heirarchial vs flat synthesis**

**Hierarchial Synthesis**

Submodule level synthesis

In a design with multiple instances we can use this to synthesize once and replicate it many times and stich together to obtain the netlist file.
On the other hand big designs can be broken down synthesised and merged later into a single netlist.

Verilog code of Half Adder is shown below. It consists of a heirarchial structure.

<pre><code>
module sub_module2 (input a, input b, output y);
assign y = a | b;
endmodule
module sub_module1 (input a, input b, output y);
assign y = a&b;
endmodule
module multiple_modules (input a, input b, input c , output y);
	wire net1;
	sub_module1 u1(.a(a),.b(b),.y(net1));  //net1 = a&b
	sub_module2 u2(.a(net1),.b(c),.y(y));  //y = net1|c ,ie y = a&b + c;
endmodule
</pre></code>

The following fig shows the heirarchy of the multiple modules.
![image](https://user-images.githubusercontent.com/67214592/183252872-7e980846-3339-453e-8071-9132dd45c3ca.png)

**Flatten Synthesis**

`flatten` is the command to flatten out the heirarchy and this is the resultant structure after removing heirarchy of the modules.

![image](https://user-images.githubusercontent.com/67214592/183252920-cbc427f7-4b50-4aeb-b379-9db203e6d678.png)

### **iii. Various Flop Coding Styles and Optimization**  
* Glitches in combinational circuits are unwanted transient output states. They are caused when the inputs are at intermediate state before reaching their final state. 
* Flops are introduced between the combinational circuits to avoid glitches in the circuit.

There are mainly three flop coding styles which are -

- Flop with asynchronous set/reset
- Flop with synchronous set/reset
- Flop with asynchronous and synchronous set/reset

#### **a. Flop with asynchronous set/reset**

The verilog code is given by the following and it is importnant to observe the inputs which are present inside always statement. 

 <pre><code>module dff_asyncres ( input clk ,  input async_reset , input d , output reg q );
always @ (posedge clk , posedge async_reset)
begin
    if(async_reset)
      q <= 1'b0;
   else
     q <= d;
end </code></pre>
	      
In this coding style asynchronous set/reset pin is not synchronized with the clock and it has got highest priority as compared to all other inputs. 
As shown in the following figure when reset is 1, irrespective of all other inputs output becomes zero.

![image](https://user-images.githubusercontent.com/67214592/183254231-d8de95dd-e2a0-4420-97c1-bd8d032e7c30.png)

As shown in the following figure when set is 1,	      
	     
![image](https://user-images.githubusercontent.com/67214592/183254410-9f5ab9d7-0178-4d4f-a822-86ef3d3ed593.png)

The following figure shows schematic of Flop with asynchronous reset. 

![image](https://user-images.githubusercontent.com/67214592/183254689-e06b7736-71fe-422b-9738-1f45bfd99535.png)
	      
The following figure shows schematic of Flop with asynchronous set. 
	      
![image](https://user-images.githubusercontent.com/67214592/183254785-2ae1ab4d-7c44-418b-848a-7a83e20406a3.png)

#### **b. Flop with synchronous set/reset**  
	      
The verilog code is given by the following and it is importnant to observe the inputs which are present inside always statement. 
	      
 <pre><code>module dff_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
always @ (posedge clk )
begin
if (sync_reset)
      q <= 1'b0;
else
      q <= d;
end
endmodule</code></pre>
	     
In this coding style asynchronous set/reset pin is synchronized with the clock and clock has got highest priority as compared to all other inputs. 
	      
As shown in the following figure when reset is 1, irrespective of all other inputs output becomes zero during the next clock edge.
	      
![image](https://user-images.githubusercontent.com/67214592/183254576-80138511-432c-426d-b074-b85126e2af35.png)	      
	      
The following figure shows schematic of Flop with synchronous reset. 
	      
![image](https://user-images.githubusercontent.com/67214592/183254869-228f9c5d-94f2-44db-8b3f-21d0108af92f.png)
	      
#### **c. Flop with synchronous and asynchronous set/reset**

The verilog code is given by the following and it is importnant to observe the inputs which are present inside always statement.

<pre><code>module dff\_asyncres\_syncres ( input clk , input async\_reset , input sync\_reset , input d , output reg q );
always @ (posedge clk , posedge async\_reset)
begin
   if(async\_reset)
      q <= 1'b0;
  else if (sync\_reset)
      q <= 1'b0;
  else	
      q <= d;
end
endmodule</code></pre>

In this coding style Din is synchronized with clock whereas asynchronous reset pin is not synchronized.

![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/DFF/DFF_asyncres_syncres.PNG)

The following figure shows synthesis schematic of the design.

![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/DFF/Synth_async_sync.PNG)

#### **d. Optimization**

The verilog code is given by the following and it is importnant to observe the inputs which are present inside the statement.  
	* In this hardware/standard cells is not necessary.

<pre><code>module mul2 (input [2:0] a, output [3:0] y);
   assign y = a * 2;
 endmodule
 
 The following figure shows synthesis schematic of the design.
 
 ![image](https://user-images.githubusercontent.com/67214592/183255244-f6f73d25-3aa4-4584-a5f0-2b03c301a188.png)
 
 The verilog code is given by the following and it is importnant to observe the inputs which are present inside the statement.  

<pre><code>module mul2 (input [2:0] a, output [5:0] y);
   assign y = a * 9;
 endmodule
 
 The following figure shows synthesis schematic of the design.
 
 ![image](https://user-images.githubusercontent.com/67214592/183255305-ad9db11d-064f-4337-a783-10b3a8719452.png)


## **3. Combinational and Sequential Optimization**
Optimization in VLSI digital circuits is required in order to design an efficient circuit in terms of area and power.

### **i. Combinational Logic Optimization**
 In combinational circuit design optimization is done at two levels.
- Constant propagation
- Boolean logic optimization
#### **a. Constant propagation**
Let consider an the following combinational circuit: 

![image](https://user-images.githubusercontent.com/67214592/183255894-5ef8704b-6638-4ba8-a9a3-236ab1955dca.png)

In the above circuit, if the input A=0, then the output is complement of C irrespective of the input B. Hence the entire circuit can be replaced by an inverter.
Let us look into somemore examples.

#### **b. Boolean logic optimization**
**Opt_Example 1:**
As an example, consider a 2:1 mux. A 2:1 mux requires two AND gates, one OR gate, and one inverter to be implemented. As a result, a total of four logic gates are required. 

Let us look into how optimization is performed with the following inputs.

![image](https://user-images.githubusercontent.com/67214592/183255910-f8331ea8-865f-4f7a-ab6d-948506aa4999.png)

<pre><code>
module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule
</code></pre>

The synthesis of the above design shows that, the 2:1 mux is replaced with an OR gate and hence results in an optimization.

![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/D3/opt_Check.PNG)

**Opt_Example 2:**

Let us consider the following mux based logic.
![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/D3/Opt_check2.PNG)

In the above logic circuit, the optimization leads to OR gate.

<pre><code>
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule
</code></pre>

![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/D3/Synt_opt_check2.PNG)

**Opt_Example 3:**

In the following example, two mux are connected to form a logic, and it requires total 8 logic gates to implement the mux.

![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/D3/Opt_check3.PNG)

In the above logic circuit, the optimization leads to three inputs AND gate.

<pre><code>
module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule
</code></pre>

![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/D3/Synt_opt_check3.PNG)

**Opt_Example 4:**

In this example, two mux and two gates are connected to form a logic.

![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/D3/opt_check4.PNG)

In the above logic circuit, the optimization leads top XNOR gate

<pre><code>
module opt_check4 (input a , input b , input c , output y);
 	assign y = a?(b?(a & c ):c):(!c);
 endmodule
</code></pre>

![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/D3/Synt_opt_check4.PNG)

