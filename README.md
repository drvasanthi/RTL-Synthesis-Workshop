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
		1. [Optimization sequential circuit using constant propagation](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#optimization-sequential-circuit-using-constant-propagation)
		2. [Sequential optimization for unused outputs](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#sequential-optimization-for-unused-outputs)

4. [**Day 4**: GLS, Blocking v/s Non-Blocking, and Synthesis-Simulation Mismatch](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#41-gls---gate-level-simulation)
	1. [GLS - Gate Level Simulation ](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#41-gls---gate-level-simulation)
	2. [Synthesis-Simulation Mismatch](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#42-synthesis-simulation-mismatch)

5. [**Day 5**: If, Case, For loop & For generate Statements](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#5-if-case-for-loop-for-generate-statements)
	1. [IF statements](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#51-if-statement) 
	2. [CASE statements](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#52-case-statement)
	3. [looping constructs](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#53-looping-constructs)

[**Contributors**](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#contributors)

[**Acknowledgement**](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#acknowledgement)

[**Contact Information**](https://github.com/drvasanthi/SKY130-RTL-Synthesis-Workshop#contact-information)


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

![image](https://user-images.githubusercontent.com/67214592/183256658-f052a2e7-60a3-4fd1-a11b-9673eab81f60.png)

**Flatten Synthesis**

`flatten` is the command to flatten out the heirarchy and this is the resultant structure after removing heirarchy of the modules.

![image](https://user-images.githubusercontent.com/67214592/183256716-61d01cbf-a6b6-4214-bc4e-69067493ca5a.png)

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
 endmodule</code></pre>
 
 The following figure shows synthesis schematic of the design.   
 
 ![image](https://user-images.githubusercontent.com/67214592/183255244-f6f73d25-3aa4-4584-a5f0-2b03c301a188.png)   
 
 The verilog code is given by the following and it is importnant to observe the inputs which are present inside the statement.  

<pre><code>module mul2 (input [2:0] a, output [5:0] y);
   assign y = a * 9;
 endmodule</code></pre>
 
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

![image](https://user-images.githubusercontent.com/67214592/183262215-b0ab2e1c-5a11-4d49-bb1f-e26ea6cda8fc.png)

In the above circuit, if the input A=0, then the output is complement of C irrespective of the input B. Hence the entire circuit can be replaced by an inverter.
Let us look into somemore examples.

#### **b. Boolean logic optimization**
**Opt_Example 1:**
As an example, consider a 2:1 mux. A 2:1 mux requires two AND gates, one OR gate, and one inverter to be implemented. As a result, a total of four logic gates are required. 

Let us look into how optimization is performed with the following inputs.

![image](https://user-images.githubusercontent.com/67214592/183262239-8153b1a6-55cc-4b83-954e-26034f557006.png)

<pre><code>
module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule
</code></pre>

The synthesis of the above design shows that, the 2:1 mux is replaced with an AND gate and hence results in an optimization.

![image](https://user-images.githubusercontent.com/67214592/183256851-1132f976-99bf-446f-8224-da5e0788f613.png)

**Opt_Example 2:**

Let us consider the following mux based logic.

![image](https://user-images.githubusercontent.com/67214592/183262258-481cf420-9377-4849-b1c6-799ea9007fde.png)

In the above logic circuit, the optimization leads to OR gate.

<pre><code>
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule
</code></pre>

The synthesis of the above design shows that, the 2:1 mux is replaced with an OR gate and hence results in an optimization.

![image](https://user-images.githubusercontent.com/67214592/183256935-ff6ae038-f28e-47c2-8aa1-2ee33474bb23.png)

**Opt_Example 3:**

In the following example, two mux are connected to form a logic, and it requires total 8 logic gates to implement the mux.

![image](https://user-images.githubusercontent.com/67214592/183262289-cf9e3e46-3f1d-4fa3-8bb7-10d281c39850.png)

In the above logic circuit, the optimization leads to three inputs AND gate.

<pre><code>
module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule
</code></pre>

The synthesis of the above design shows that, the 2:1 mux is replaced with an 3-input AND gate and hence results in an optimization.

![image](https://user-images.githubusercontent.com/67214592/183257127-e0f878e8-dec0-4191-842b-47bd6a53bbda.png)

**Opt_Example 4:**

In this example, two mux and two gates are connected to form a logic.

![image](https://user-images.githubusercontent.com/67214592/183262316-e8522aea-6e16-4c92-86a2-23ecf6cb1f3c.png)

In the above logic circuit, the optimization leads top XNOR gate

<pre><code>
module opt_check4 (input a , input b , input c , output y);
 	assign y = a?(b?(a & c ):c):(!c);
 endmodule
</code></pre>

The synthesis of the above design shows the XNOR gate and hence results in an optimization.

![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/D3/Synt_opt_check4.PNG)

### **ii. Sequential Logic Optimization**

- Constant Propagation
- Retiming 
- Cloning
- State optimization

We will restrict our discussion to sequential logic optimization in constant propagation.

#### **a. Optimization sequential circuit using constant propagation**

**Sequential Example-1**

Consider a sequential circuit shown below

![image](https://user-images.githubusercontent.com/67214592/183262339-4879f56f-43d0-4e79-8ff7-c583c45bfa8b.png)

In the above circuit, if asynchronous reset is enabled then Q = 0 irrespective of clock, else Q =1 since D input is set to 1. 

The same can be verified in the simulated waveform shown below with verilog code.

<pre><code>
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end
endmodule
</pre></code>

![image](https://user-images.githubusercontent.com/67214592/183257851-d710d1e0-2bf5-4347-8d67-f3f46972e040.png)

The following figure shows the synthesis of the above circuit. As it can be seen in the above figure no optimization can be done with the design.

![image](https://user-images.githubusercontent.com/67214592/183258086-2ed3b8d2-a292-468b-99bc-2ae50fefac50.png)

**Sequential Example-2**

Consider an another sequential circuit shown below

![image](https://user-images.githubusercontent.com/67214592/183262384-4f0c4789-ff30-42e7-98d0-7bac64d9efea.png)

In the above circuit, if the asynchronous set is enabled then Q = 1 and the output remains at the same state, since D input is set to 1. The same can be verified in the simulated waveform shown below along with verilog.

<pre><code>
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end
endmodule
</pre></code>


![image](https://user-images.githubusercontent.com/67214592/183258039-66f78161-8fde-4ff4-9aaf-c9dba3e89e32.png)

As shown in the wave form, the output remains at logic 1, irrespective of states of the other inputs. Hence the above design can be replaced by a simple buffer there by optimizing power and area.

The following figure shows the synthesis of the above circuit. As it can be seen in the synthesis design, optimization is performed by in synthesis stage by replacing the entire design by a simple wire buffer.

![image](https://user-images.githubusercontent.com/67214592/183258146-fa8e158b-a18b-4d57-969a-d504eb020112.png)

**Sequential Example-3**

Consider an another sequential circuit shown below

![image](https://user-images.githubusercontent.com/67214592/183262430-6c74e1ec-2858-4396-8a0c-5ffe43a9fb62.png)

The above circuit consists of two asynchronous set and reset DFF. Hence the optimization can't be done in the above design. 


The following figure shows the synthesis of the above circuit along with verilog code. As it can be seen in the synthesis design, optimization is performed  in synthesis stage by replacing the entire design by a simple wire buffer.

<pre><code>
module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end
</pre></code>

![image](https://user-images.githubusercontent.com/67214592/183258213-623e49c5-4b41-427c-a7a0-a97ee326183c.png)

![image](https://user-images.githubusercontent.com/67214592/183258277-16032541-531b-4abd-a6a6-6151ca571935.png)

**Sequential Example-4**

In the design sequential example - 3, the optimization can be achieved by replacing asynchronous **reset DFF** by asynchronous **set DFF** which is as shown in the below example.

![image](https://user-images.githubusercontent.com/67214592/183262456-db16bfd5-c102-424d-976e-d38ca71ed969.png)

The above circuit consists of two asynchronous set DFF's. Hence the output remains at logic irreseprctive of clock. Hence optimization in the above design results in a buffer. 


The following figure shows the synthesis of the above circuit along with the code. As it can be seen in the synthesis design, the two flipflops are replaced by two buffers.

<pre><code>
module dff_const4(input clk, input reset, output reg q);
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

endmodule
</pre></code>


![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/D3/synt_seq4.PNG)

#### **b. Sequential optimization for unused outputs**

![image](https://user-images.githubusercontent.com/67214592/183262493-4c5e59b4-2c2a-4860-a036-eb5580538e5f.png)

Let us consider following verilog code of an up counter.

<pre><code>

module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = count[0];

always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end

endmodule
			
</pre></code>

In the above example, the output is assigned to LSB of counter value. Hence we can optimize the design for the required output so that additional hardware overhead can be minimized.
			
The following figure show the synthesized output of the above logic. 

![image](https://user-images.githubusercontent.com/67214592/183258493-73857324-1698-4e5d-9ae1-1585edd8fde4.png)

As shown in the above figure, only one DFF is utilized in the design in contrast to 3-DFF's for a 3-bit counter. Hence the optimization results in reduced area and power. 

## **4. GLS, Blocking v/s Non-Blocking, and Synthesis-Simulation Mismatch**

### **i. GLS - Gate level simulation**  
* GLS stands for Gate level simulation.   
* It is used to verify the logical correctness of design after synthesis.  
* It also ensures the timing of the design is met. The GLS needs to be run with delay annotation.

The below figure shows the GLS using iverilog

![image](https://user-images.githubusercontent.com/67214592/183258753-a445291c-e29e-40a8-b44d-aef41951ea9e.png)

Let us consider an example, the following code shows logic of ternary operator.
<pre><code>

module ternary_operator_mux (input i0 , input i1 , input sel , output y);
	assign y = sel?i1:i0;
	endmodule
	
</pre></code>

The following commands are executed to simulate the design

```
iverilog ternary_operator_mux.v tb_ternary_operator_mux.v 
./a.out
gtkwave tb_ternary_operator_mux.vcd 
```
The following image shows the simulation of ternary operator. It can observed in the waveform window, the logic of ternary operator is same as 2:1 mux.

![image](https://user-images.githubusercontent.com/67214592/183258803-c604918c-b111-4087-8be0-7276c0ee4386.png)

Now, let us perform Gate level simulation of ternary operator. 

The following code is used to generate Gate Level Netlist.

```
read_liberty -lib ./my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog ./verilog_files/ternary_operator_mux.v 
synth -top ternary_operator_mux 
show
history
abc -liberty ./my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
write_verilog -noattr ternary_mux_netlist.v
```
The following figure shows the synthesis of ternary mux

![image](https://user-images.githubusercontent.com/67214592/183258858-6ca9e436-98a2-4ff1-a72e-9c4825c961ab.png)

```
iverilog ./my_lib/verilog_model/primitives.v ./my_lib/verilog_model/sky130_fd_sc_hd.v ternary_mux_netlist.v ./verilog_files/tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```

The above code is used simulated gate level netlist by importing primitives library into verilog.
The resultant waveform is shown below. It can be observed Gate level simulation matches with RTL simulation.

![image](https://user-images.githubusercontent.com/67214592/183258935-15e5d711-34e3-4a08-9236-7aec6fa10c85.png)

### **ii. Synthesis Simulation Mismatch**

 Synthesis Simulation Mismatch(SSM) is mainly due to two reasons.
 - Missing sensititivity list
 - Blocking and non blocking statements
 
**a. Missing Sensitivity list**

Let us look into the following verilog code example
```

module bad_mux (input i0 , input i1 , input sel , output reg y);
always @ (sel)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```

In the above code, sensitivity list includes only the select line, hence output is not updated even though the inputs changes. This is observed in the simulation waveform below.

![image](https://user-images.githubusercontent.com/67214592/183259093-a75f1bb2-9017-4883-af48-e79c5d458cf0.png)

Now, let us look into gate level simulation of the above design.
The following commands are used to generate gate level netlist.
```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog bad_mux.v 
synth -top bad_mux 
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
write_verilog bad_mux_netlist.v
```
The following execution of commands is performed for GLS 

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_netlist.v tb_bad_mux.v
   ./a.out
   gtkwave tb_bad_mux.vcd
```
The GLS simulation waveform is shown below.
![image](https://user-images.githubusercontent.com/67214592/183259143-a0e2bceb-04e0-4688-9ead-a834cabd8b08.png)

From the above synthesis waveform, there is a mismatch synthesis and simulation waveform. This is mainly due to signals in the sensitivity list.

 **b. Blocking and Non Blocking statements**

In a verilog code, blocking statements are in sequential order, where as non blocking statements are executed in concurrent fashion.

* Inside always block  
 `= Blocking`  
     * Executes the statement in the order it is written.  
     * So the first statement is evaluated before the second statement.  
  `<= Non-Blocking`  
     * Executes all RHS when always block is entered and assign to LHS.  
     * Parallel Evaluation.  
     
let us consider the follwoing verilog example code.
```
module blocking_caveat (input a , input b , input  c, output reg d); 
reg x;
always @ (*)
begin
	d = x & c;
	x = a | b;
end
endmodule

```

In the above example the output d is evaluated first and x is evaluated next. Therefore the output d is evaluated based on the previous value of x. This creates a mismatch between Synthesis and Simulation output.

The following figure shows the simulation output of above code. As it can be seen in the output waveform, the output y is evaluated based on the previous values of a and b.

![image](https://user-images.githubusercontent.com/67214592/183259330-8ce21bfe-25de-44b0-aeb4-891b8f8d0f8c.png)

![image](https://user-images.githubusercontent.com/67214592/183259400-91bbebaa-e313-4ab0-bf8f-73d1582a7861.png)

The following figure shows the simulation output based on the Gate level netlist. The waveform shows the correct execution of the output as compared to the previous output.

![image](https://user-images.githubusercontent.com/67214592/183259420-e5459f75-986e-403e-a9b3-ac17afb12c3a.png)

## **5. If, Case, For loop & For generate Statements**

### **i. If Statement**

If statements are the highest priority conditional statements. They invoke MUX when written properly else they `Inferred Latches` (incomplete if statement).

Consider an example code below.
```
if(cond1)
	begin 
		state1
		
	end
elseif(cond2)
	
	begin
		state2
	end
else
	begin 
		state2
	end
endif
```

The below figure shows the equivalent logic circuit using mux

![image](https://user-images.githubusercontent.com/67214592/183262548-b43ce0fd-f1e6-4289-bc0a-342cc7c5de19.png)

Now, let us consider the cases where if constructs are not written properly.

**Example1-incomplete_if:**

Consider the below verilog code.

```
module incomp_if (input i0 , input i1 , input i2 , output reg y);
always @ (*)
begin
	if(i0)
		y <= i1;
end
endmodule
```
In the above example if structure is incomplete. Let us check its waveform and synthesized output.

As shown in the waveform below, output retains its previous state if i0=0, hence it acts like a latch.

![image](https://user-images.githubusercontent.com/67214592/183259704-068f3ca3-40e4-46bc-a573-ac86c35768fe.png)

Synthesized output shows D latch connected between input and output.

![image](https://user-images.githubusercontent.com/67214592/183259729-eee734cc-6b7b-4d0a-9c78-c63bbf874f16.png)


**Example2-incomplete_if2:**

Consider a verilog code shown below.

```
module incomp_if2 (input i0 , input i1 , input i2 , input i3, output reg y);
always @ (*)
begin
	if(i0)
		y <= i1;
	else if (i2)
		y <= i3;
end
endmodule

```

Figure below shows the simulated waveform and synthesis results of the above code. In this we can observe when both I0 and I2 are zero, the output remains at either 0 or 1.

![image](https://user-images.githubusercontent.com/67214592/183259836-b6eeeb2b-eeb6-4a97-9321-1c3cfe89d7f2.png)

Synthesized output shows D latch with combinational logic and OR gate

![image](https://user-images.githubusercontent.com/67214592/183259886-8e8f3ff4-3f23-44d5-bdf0-7742841210d6.png)

### **ii. CASE Statement**

Case statements are mapped to mux when they are synthesized. In the case statements also infers latches when its not written properly.

Let us try to understand this by taking an example of a complete case statement and an incomplete case statement.

**Example1-incomp_case:**

Given below is the code of an incomplete case statement example which will result in an inferred latch.

```
module incomp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
always @ (*)
begin
	case(sel)
		2'b00 : y = i0;
		2'b01 : y = i1;
	endcase
end
endmodule
```

As shown in the above code, only two conditons of sel line is specified and hence in an inferred latch.

The following figure shows simulated waveform and synthesis output. As it can be seen in simulated output, output is latched for 10 and 11 conditions.

![image](https://user-images.githubusercontent.com/67214592/183259950-160105fe-5849-4bdf-bd46-db158e26cf15.png)

It can be seen in the synthesis output, D-latch is present at the output.

![image](https://user-images.githubusercontent.com/67214592/183259976-8e087b46-52f9-48ae-9dec-adeeb1253350.png)

**Example2-comp_case:**

consider a following code.

```
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

```
In the above code the missing conditions are taken care by default statement. Also simulation of above code shown below.

![image](https://user-images.githubusercontent.com/67214592/183260076-19c22eca-8009-4158-b42e-bc9f5042893f.png)

And also it can be observed from the synthesized output, no D latch is inferred.

![image](https://user-images.githubusercontent.com/67214592/183260107-19fe9950-6c3f-4591-8a91-8182c62d8445.png)

**Example3-partial_case_assign:**

consider a following code.

```
module partial_case_assign (input i0 , input i1 , input i2 , input [1:0] sel, output reg x, output reg y);
always @ (*)
begin
	case(sel)
		2'b00 : begin
			y = i0;
			x = i2;
		2'b01 : y = i1;
		default : begin
			x = i1;
			y = i2;
	endcase
end
endmodule

```
The following figure shows simulated waveform and synthesis output. As it can be seen in simulated output, output is latched for 01 conditions.



It can be seen in the synthesis output, D-latch is present at the output.

![image](https://user-images.githubusercontent.com/67214592/183260234-e371316a-0f61-40af-9cf6-ceddb210758d.png)


### **iii. Looping constructs**

There are two types of looping constructs 

- for loop constructs
- for generate loop constructs

**a. for loop constructs**

*for* loops are placed inside the always statement. This loop is not going to instantiate any hardware.

**Example1-mux_generate:**

```
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
```

The above code represents a 4:1 Mux. The same can be verified by synthesizing this design.

Below figure shows the RTL simulation.

![image](https://user-images.githubusercontent.com/67214592/183260518-a9110eb9-f4f4-401f-9a0a-0e689fef0671.png)

The figure below shows synthesized output of the above code.

![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/mux_generate.PNG)

**b. for generate loop constructs**

*for* generate statements are used to instantiate a hardware module for a large number of instantiations. Ex: to instantiate an AND gate 100 times. They should never be used inside an always block.

An example of using for generate statements is given below. We use generate statements and for loop to implement an 8-bit Ripple Carry Adder which uses multiple instantiations of Full Adder block.

```
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
endmodule

```
		
The following figure shows the output of simulation. 

![image](https://user-images.githubusercontent.com/67214592/183260651-a3f2f096-9f9b-4f51-9cf4-2fcd06fea458.png)
		
The following figure shows the synthesised output in which FA modules are instantiated.
		
![](https://github.com/mrshashi4u/RTL-Design-and-Synthesis/blob/main/D5/rca_synth.PNG)
		
		

## **Contributors**

  * Vasanthi D R
  * Kunal Ghosh

## **Acknowledgement**
  
  * Kunal Ghosh, Director, VSD Corp. Pvt. Ltd.

## **Contact Information**

  * Vasanthi D R, PhD Scholar, International Institute of Information Technology, Bangalore vasanthidr11@gmail.com
  * Kunal Ghosh, Director, VSD Corp. Pvt. Ltd. kunalghosh@gmail.com




