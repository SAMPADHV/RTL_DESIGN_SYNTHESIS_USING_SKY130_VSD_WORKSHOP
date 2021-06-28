# RTL_DESIGN_SYNTHESIS_USING_SKY130_VSD_WORKSHOP
Repo of Workshop conducted by Team VSD RTL_Design_Synthesis_using sky180 
![image](https://user-images.githubusercontent.com/69497292/123116528-9c589f00-d45e-11eb-8b74-f587b1ba64f8.png)

Details Of Work :

Day 1: 

* Basic Introduction to iverilog
* Tool Flow
* Concepts of Synthesis
* Delay, Power, Area Relations wrt Design

Day 2:

* PVT characteristics
* LIB file details
* Hierarchial and Flatten Synthesis
* Submodule level synthesis
* Why Flipflops
* Asynchronous and Synchronous Flops
* special cases


Day 3:
Day 4:
Day 5:

## Day 1:
* Started with Defining Simulator,Design,Testbench

Working of Simulator:
Simulator checks for any change in the input and ouput is evaluated

stimulus_Generator >>>>  Design  >>>>>> Stimulus Observer
* Flow:

![image](https://user-images.githubusercontent.com/69497292/123119160-e773b180-d460-11eb-8425-b85f579dbb62.png)

As in above pic Directory named VLSI is created. Files required are cloned, LIB Files and Experiment files are checked

![image](https://user-images.githubusercontent.com/69497292/123119826-7b457d80-d461-11eb-89be-0432b901dc9c.png)

Files available before conduction of experiments.

![image](https://user-images.githubusercontent.com/69497292/123120512-0292f100-d462-11eb-9453-2c3083043f46.png)

Once the rtl and testbench are fead to iverilog you can observe the file a.out created as an output details of which is explained later

![image](https://user-images.githubusercontent.com/69497292/123121232-9f558e80-d462-11eb-908e-fd6111c86dcb.png)

once a.out is executed it gives out .vcd file.

![image](https://user-images.githubusercontent.com/69497292/123121489-d3c94a80-d462-11eb-8cd8-744448562c6d.png)

![image](https://user-images.githubusercontent.com/69497292/123121742-0a9f6080-d463-11eb-918c-d600f0ef55a8.png)

Now with this we can observce  the simulation waveform using gtkwave

The codes of goodmux.v and tb_goodmux.v are as follows:

![image](https://user-images.githubusercontent.com/69497292/123122070-53efb000-d463-11eb-9301-2c58637e0c79.png)

![image](https://user-images.githubusercontent.com/69497292/123122176-6a960700-d463-11eb-8f32-5c9ab7125164.png)

* Yosys

RTL + liberate file >>>> yosys >>>> netlist file

Yosys is a synthesizer which converts rtl to gate level netlist wrt to standard cell available

Once the Synthesis is done we again verify the functionality of netlist using iverilog 

netlist + testbench >>>> iverilog >>>> vcd file ( observed using gtkwave)

LIB:

Lib file contains the details of all the standard cell available. Their are different types of cells

1. Fast cells: These are used to  reduce Propagation Delay. With decrease in Pd We can have high frequency operation
2. Slow cells: They increase the Delay. These are essential to remove hold violations

High Speed : More Width : Increase in area : High current : High Power Dissipiation
Low Speed  : Lesser Width : lesser area: Less Current : lesser  Power Dissipiation

Below are the commands and their resuls of synthesis:

1. Invoke yosys:

![image](https://user-images.githubusercontent.com/69497292/123124318-34598700-d465-11eb-95e0-f8d40526f323.png)

2. Reading the lib file :

![image](https://user-images.githubusercontent.com/69497292/123124466-53f0af80-d465-11eb-8b35-46a8a1891840.png)

location path should be corrctly provided

3. Read Verilog :

![image](https://user-images.githubusercontent.com/69497292/123125739-6ae3d180-d466-11eb-9fc2-41cd3ac41a28.png)

4. Synthesis :

![image](https://user-images.githubusercontent.com/69497292/123127911-5274b680-d468-11eb-83e7-dd89a0007fc9.png)

![image](https://user-images.githubusercontent.com/69497292/123132802-c022e180-d46c-11eb-8938-830c5a0bbab1.png)

![image](https://user-images.githubusercontent.com/69497292/123133055-fceed880-d46c-11eb-952d-1fdfc5438895.png)

5. genearating netlist:

![image](https://user-images.githubusercontent.com/69497292/123133252-2dcf0d80-d46d-11eb-8fdd-01cb25cd54d4.png)

![image](https://user-images.githubusercontent.com/69497292/123134476-71764700-d46e-11eb-9ce9-40d6d8374658.png)

6. Netlist Pictorial rep:
7. 
![image](https://user-images.githubusercontent.com/69497292/123135139-142ec580-d46f-11eb-982b-4d303b2c4d53.png)

![image](https://user-images.githubusercontent.com/69497292/123134988-f3ff0680-d46e-11eb-87f5-2c9446973b34.png)

7.Netlist verilog code:

without attribute: Will have some additional / Extra details

![image](https://user-images.githubusercontent.com/69497292/123135943-0463b100-d470-11eb-9004-6184ba6bf562.png)

Netlist :
![image](https://user-images.githubusercontent.com/69497292/123136053-21987f80-d470-11eb-8417-c0d2fc9ead6b.png)

![image](https://user-images.githubusercontent.com/69497292/123137274-6cff5d80-d471-11eb-857b-372cca8757bc.png)

With attribute : will be filtered one with specific connection details

![image](https://user-images.githubusercontent.com/69497292/123136569-b602e200-d470-11eb-91ab-19266a71b265.png)

![image](https://user-images.githubusercontent.com/69497292/123137171-535e1600-d471-11eb-904e-e77780b0205f.png)



# DAY 2

Some of the  useful vim commands

* gvim ..... address  :- To open a vim editor
* "i" To insert
* :syn off To remove highlight of syntax
* :se hls < enter> /<name> :- To search in vim
* :se num :- To Enable line no
* :vsp :- vertical split of vim
* :sp :- horizontal split
* -o helps us to open two or more files at once
  
PVT Conditions
  
  Process Variations: variations which are due to fabrication 
  Voltage Variations: variation wrt change in voltage
  Temperature Variations: Semiconductors are sensitive to temperature.
 
  These together characterise the chip. While designing chips all these variations have to be kept in mind
  These details are present in the LIB files
  LIB Files:
  * They have details of units used in files
  * operating conditions 
  * standard cells
  * Delay model used
  * Delay and Power Details of all posssible input conditions
  
 Synthesis:
  Hierarchial Synthesis : Synthesis will have netlist in terms of submodules.
  Flat Synthesis : Synthesis will be done in terms of gates.
  
 Submodule Synthesis:
  Submodule level synthesis can also be done wrt individual modules
  advantages:
  * When you have multiple modules of same instances you can verify synthesis of one and can instantiate others wrt requirement
  * We can easily divide the work in larger design and complete the work
  
 Why Flop:
  When we have a combinational circuit we will always have a glitch due to difference in propagation delay at inputs.
  
  With multiple combinational circuits output might never settle down ,so flops are used to store data and it prevents propagation of glitches 
  
 Synchronous and Asynchronous Circuit:
 
 Synchronous Circuits: Circuits whose outputs changes only wrt clocks posedge or negedge.
 
 Asynchronous Circuits: Circuits which have set/reset/both in sensitivity list along with clocks.
  
  
Some Special cases:
  Some optimization techniques synthesis tool takes:
  
  * Multiplying with powers of 2:
  Here we expect multiplier circuit in netlist but we don't get any hardware for doing things. 
  a*2 ={a,0}
  
  Snapshots of the work :
  
  * lib file 
  ![image](https://user-images.githubusercontent.com/69497292/123581282-30c55780-d7f9-11eb-923b-88ee49de66b5.png)

  ![image](https://user-images.githubusercontent.com/69497292/123581467-9ca7c000-d7f9-11eb-87b9-487d76ee679c.png)

  ![image](https://user-images.githubusercontent.com/69497292/123581493-a7625500-d7f9-11eb-9729-f21cfaf292bd.png)

  ![image](https://user-images.githubusercontent.com/69497292/123581528-bf39d900-d7f9-11eb-9c28-d148cc93fde2.png)

  ![image](https://user-images.githubusercontent.com/69497292/123581580-d5479980-d7f9-11eb-851f-fdcbb7c78af3.png)

  ![image](https://user-images.githubusercontent.com/69497292/123581631-f01a0e00-d7f9-11eb-9095-af278bb3ac46.png)

  ![image](https://user-images.githubusercontent.com/69497292/123581689-0758fb80-d7fa-11eb-8950-a76620c121c3.png)
  
![image](https://user-images.githubusercontent.com/69497292/123581763-33747c80-d7fa-11eb-8ae0-c382fb00ea60.png)
  
  ![image](https://user-images.githubusercontent.com/69497292/123581824-4be49700-d7fa-11eb-9ea5-79c8e3671434.png)

  ![image](https://user-images.githubusercontent.com/69497292/123582406-60755f00-d7fb-11eb-85ea-e3bba37cb84e.png)

  ![image](https://user-images.githubusercontent.com/69497292/123583966-2d809a80-d7fe-11eb-8109-409099ce4d7b.png)

  ![image](https://user-images.githubusercontent.com/69497292/123584034-4b4dff80-d7fe-11eb-9ea1-94b41af9a3e0.png)

  ![image](https://user-images.githubusercontent.com/69497292/123584152-7df7f800-d7fe-11eb-92b7-c9a77cba2649.png)

  Multiple Modules:
  








