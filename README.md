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

* Combinational logic Optimization
  * Constant Propagation
  * Boolean logic Optimization
* Sequential logic Optimization
  * Basic
    Sequential Constant propagation
  * Advance
    State Optimization
    Retiming
    Sequential logic cloning
  

Day 4:

  * Gate level Simulation
  * Synthesis simulatiion mismatch
  * Missing Sensitivity list 
  * Blocking and NonBlocking statements
  * Caviates with Blocking statements
  
Day 5:

  * Infered latches
  * if , case caviates
  * Looping constructs
  
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



## DAY 2

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

  * Multiple Modules:
  
![image](https://user-images.githubusercontent.com/69497292/123584383-e6df7000-d7fe-11eb-8e64-592fb50c39ff.png)

![image](https://user-images.githubusercontent.com/69497292/123584633-5a817d00-d7ff-11eb-876f-c75979012bbb.png)

  ![image](https://user-images.githubusercontent.com/69497292/123584878-c49a2200-d7ff-11eb-9c3e-503d36fcf082.png)

 
![image](https://user-images.githubusercontent.com/69497292/123587341-c6fe7b00-d803-11eb-940e-f118595179ae.png)

 ![image](https://user-images.githubusercontent.com/69497292/123587412-dda4d200-d803-11eb-8dbe-99cb655f6753.png)
![image](https://user-images.githubusercontent.com/69497292/123587505-0331db80-d804-11eb-83a6-55317d5f0d55.png)

  ![image](https://user-images.githubusercontent.com/69497292/123587620-278db800-d804-11eb-92ba-dffcdc295774.png)
  
  * Sub Modules
  ![image](https://user-images.githubusercontent.com/69497292/123590582-72a9ca00-d808-11eb-92a2-48f371f6f1ad.png)

  ![image](https://user-images.githubusercontent.com/69497292/123590594-763d5100-d808-11eb-99fd-3b7e6c892a36.png)

![image](https://user-images.githubusercontent.com/69497292/123590679-94a34c80-d808-11eb-875b-e7fdb24b174a.png)

  ![image](https://user-images.githubusercontent.com/69497292/123590752-b1d81b00-d808-11eb-9304-fd4c8dd8b97a.png)



  * Hierarchial level synthesis
  
  ![image](https://user-images.githubusercontent.com/69497292/123587711-4d1ac180-d804-11eb-8fac-79e6c5643a41.png)

![image](https://user-images.githubusercontent.com/69497292/123587777-66237280-d804-11eb-855c-89baaa1cdfe5.png)

  ![image](https://user-images.githubusercontent.com/69497292/123587813-74718e80-d804-11eb-8513-f646393b1b39.png)

  * Flattening:
  
  ![image](https://user-images.githubusercontent.com/69497292/123587862-87845e80-d804-11eb-9380-af2e4e58b364.png)

  ![image](https://user-images.githubusercontent.com/69497292/123587885-91a65d00-d804-11eb-8515-10f067c44345.png)

  ![image](https://user-images.githubusercontent.com/69497292/123587954-aa167780-d804-11eb-98eb-72d4a7d2f60f.png)

  ![image](https://user-images.githubusercontent.com/69497292/123587970-b3074900-d804-11eb-9820-1a5ff432d115.png)

  * Synchronous and Asynchronous Flipflops
  
  ![image](https://user-images.githubusercontent.com/69497292/123588124-eea21300-d804-11eb-9232-cf8826cfe79c.png)

  ![image](https://user-images.githubusercontent.com/69497292/123588182-037ea680-d805-11eb-9c9f-953e756f42c3.png)

  ![image](https://user-images.githubusercontent.com/69497292/123588233-14c7b300-d805-11eb-8fd5-efe2f963de45.png)

  ![image](https://user-images.githubusercontent.com/69497292/123588285-290bb000-d805-11eb-94f4-45cfb91d2634.png)
  
  ![image](https://user-images.githubusercontent.com/69497292/123588805-f6ae8280-d805-11eb-8054-29b622f76f24.png)

  ![image](https://user-images.githubusercontent.com/69497292/123588889-12b22400-d806-11eb-8734-b1561664d398.png)

  ![image](https://user-images.githubusercontent.com/69497292/123589025-3ffed200-d806-11eb-9931-918c3cc2d390.png)
  ![image](https://user-images.githubusercontent.com/69497292/123590276-1050c980-d808-11eb-904c-fd500bca0e33.png)

  ![image](https://user-images.githubusercontent.com/69497292/123590313-1b0b5e80-d808-11eb-851b-53af06504003.png)


  ![image](https://user-images.githubusercontent.com/69497292/123589496-f19e0300-d806-11eb-895a-f6d7abfd8a0d.png)

  ![image](https://user-images.githubusercontent.com/69497292/123589537-fe225b80-d806-11eb-8f29-af5be5368de2.png)
  
  ![image](https://user-images.githubusercontent.com/69497292/123590000-ae905f80-d807-11eb-99d4-0c52f525cd7e.png)

  ![image](https://user-images.githubusercontent.com/69497292/123590030-b7813100-d807-11eb-8042-a4a43ae4cf1e.png)

  ![image](https://user-images.githubusercontent.com/69497292/123590066-c667e380-d807-11eb-94d5-4d0708b73ea0.png)

  ![image](https://user-images.githubusercontent.com/69497292/123590107-d2ec3c00-d807-11eb-8b33-7115e6c29739.png)

  *special cases
  
  ![image](https://user-images.githubusercontent.com/69497292/123590848-ddf39c00-d808-11eb-80b8-d06efbe59ced.png)

  ![image](https://user-images.githubusercontent.com/69497292/123590874-ea77f480-d808-11eb-9e43-6b838da12912.png)

  ![image](https://user-images.githubusercontent.com/69497292/123590956-08ddf000-d809-11eb-9d39-f12f4c147af6.png)

  ![image](https://user-images.githubusercontent.com/69497292/123591265-607c5b80-d809-11eb-8e07-cc932d2b85dc.png)

  ![image](https://user-images.githubusercontent.com/69497292/123591347-7722b280-d809-11eb-89a9-00e20a020409.png)
  
  ![image](https://user-images.githubusercontent.com/69497292/123591408-8e61a000-d809-11eb-8c7e-c221eb52da22.png)

  ![image](https://user-images.githubusercontent.com/69497292/123591590-cff24b00-d809-11eb-8db0-a16597cbcab3.png)
  
## DAY 3
  
  * Combinationl Logic Optimization
  
  Constant optimization:
  
  Here we optimize the design to get optimised area and power
  Examples can be seen in below screenshots
  command used: opt_claen -purge 
  
  Boolean logic Optimization 
  
  Expressions are solved and simplified equation is obtained. This is similar to kmap optimization but done without kmap implementation.
  
  * Sequential logic Optimization
  
  Basic : Sequential Constant Propagation
  
  some times the code written is such that it represents flipflop logic but the output wont depend on the flop input then the flip flop will not be considered in symthesis
  
  Advanced:
  State optimization: This includes optimization of unused states
  
  cloning : This technique is used when we do physical aware synthesis
  
  Retiming: This involves  shifting of combinational logic to next flop or previous flops keeping in mind a slack at flops. 
  
  * Combinational optimization :
  before optimizing
  
  ![image](https://user-images.githubusercontent.com/69497292/123596439-d1bf0d00-d80f-11eb-8d72-0248d070fa1e.png)

  ![image](https://user-images.githubusercontent.com/69497292/123596491-e1d6ec80-d80f-11eb-9f8c-c53728a73b08.png)
  
  ![image](https://user-images.githubusercontent.com/69497292/123596717-25315b00-d810-11eb-960c-3dccec2d716b.png)

  after optimizing
  
  ![image](https://user-images.githubusercontent.com/69497292/123596545-f4512600-d80f-11eb-85f9-d43237026eb0.png)
  
  ![image](https://user-images.githubusercontent.com/69497292/123596771-34180d80-d810-11eb-91bc-50674d008702.png)

  ![image](https://user-images.githubusercontent.com/69497292/123596890-56119000-d810-11eb-9c16-8381bb7a27c7.png)

  ![image](https://user-images.githubusercontent.com/69497292/123597046-793c3f80-d810-11eb-8473-7a07b3f573a8.png)

  * Sequential Optimization
  
  ![image](https://user-images.githubusercontent.com/69497292/123597620-2fa02480-d811-11eb-975e-0f535108479c.png)

  ![image](https://user-images.githubusercontent.com/69497292/123597659-3d55aa00-d811-11eb-9aa5-5dba51574e8c.png)

  ![image](https://user-images.githubusercontent.com/69497292/123597717-4f374d00-d811-11eb-9b43-83f032c8997b.png)

  ![image](https://user-images.githubusercontent.com/69497292/123597841-768e1a00-d811-11eb-832d-4d31158e0454.png)

  ![image](https://user-images.githubusercontent.com/69497292/123597877-8279dc00-d811-11eb-8afd-edf5bbeb973a.png)
 
![image](https://user-images.githubusercontent.com/69497292/123598426-21063d00-d812-11eb-8de9-72dc52712db4.png)

  ![image](https://user-images.githubusercontent.com/69497292/123598436-25325a80-d812-11eb-9e34-9e8e74c1372e.png)

  ![image](https://user-images.githubusercontent.com/69497292/123598485-34b1a380-d812-11eb-908d-c6ed32589ffd.png)

  ![image](https://user-images.githubusercontent.com/69497292/123598525-3f6c3880-d812-11eb-80bb-6732cef1ad64.png)

![image](https://user-images.githubusercontent.com/69497292/123598688-64f94200-d812-11eb-99eb-2e9ed9cf1dd3.png)

  ![image](https://user-images.githubusercontent.com/69497292/123598765-7e01f300-d812-11eb-9e3c-c49cb75362b7.png)

  ![image](https://user-images.githubusercontent.com/69497292/123598884-a12ca280-d812-11eb-8cae-f4d39dfdbc0f.png)

  ![image](https://user-images.githubusercontent.com/69497292/123598939-ad186480-d812-11eb-9428-6e314cc3e7f7.png)

  ![image](https://user-images.githubusercontent.com/69497292/123599005-b9042680-d812-11eb-922b-883baac59bc1.png)

  Unused output optimization in sequential circuits:
  
  ![image](https://user-images.githubusercontent.com/69497292/123599147-ebae1f00-d812-11eb-9395-d2aca5420d1f.png)
  
  ![image](https://user-images.githubusercontent.com/69497292/123599297-1304ec00-d813-11eb-80f2-db1b95e5b357.png)

  ![image](https://user-images.githubusercontent.com/69497292/123599432-36c83200-d813-11eb-9d3e-8ca1293c9519.png)

  ## DAY 4
  
  * Gate level simulation :
  
  Here the generated netlist is tested by simulating. Some times the generated netlist does not match the functionality, So Gate level simulation plays an important role in vlsi design flow.
  
  Why GLS: 
  
  * To verify  the functionality after synthesis
  * To check if the timing of design is met
  
   netlist (.v) file + tb + gate_level_verilog_model <<< iverilog <<< vcd file which is further observed
 
 gate_level_veriog_models are of two types:
 
 Timing aware : which has both fuctionality and timimg details
 Functional : This only has details of functionality only functional velidation can be done
  
  RTL file will not be having details in terms of standard cell so earlier thier was no need of gate_level_verilog_model to verify but now we are verifying the netlist which has the code in terms of standard cells. So now we had to add a referance file , so that iverilog gets the  referance file for these standard cells.
  
  (((HERE IN THIS WORKSHOP WE HAVEN'T CONSIDERED TIMING AWARE MODELS)))
  
 one might think when the netlist created is of rtl itself then why there would be a difference in functionality. What are the possible mismatches, they are due to 
 * Missing Ssensitivity list
 * Difference in blocking and non blocking assignment
 * Non standard verilog coading style
 
![image](https://user-images.githubusercontent.com/69497292/123614250-c70d7380-d821-11eb-8da5-b46dd3de44ab.png)

 ![image](https://user-images.githubusercontent.com/69497292/123614319-d8ef1680-d821-11eb-9cf7-07a0d1661b10.png)

 ![image](https://user-images.githubusercontent.com/69497292/123614371-e5736f00-d821-11eb-9713-8e97d57c6b22.png)

 ![image](https://user-images.githubusercontent.com/69497292/123614456-f7551200-d821-11eb-80ac-1e0385673424.png)

 ![image](https://user-images.githubusercontent.com/69497292/123614502-08058800-d822-11eb-8a3e-0e1d3c3f20d8.png)

 ![image](https://user-images.githubusercontent.com/69497292/123614546-13f14a00-d822-11eb-9ed4-101d810e636f.png)

 ![image](https://user-images.githubusercontent.com/69497292/123614650-27041a00-d822-11eb-92c3-ab5665b33102.png)

 ![image](https://user-images.githubusercontent.com/69497292/123614747-3c794400-d822-11eb-8509-42e91d6f4c16.png)

 ![image](https://user-images.githubusercontent.com/69497292/123614821-4ef37d80-d822-11eb-8229-e2f6c4e4df7f.png)
 
![image](https://user-images.githubusercontent.com/69497292/123614987-7d715880-d822-11eb-9e13-c523dd31144f.png)
 
 ![image](https://user-images.githubusercontent.com/69497292/123615146-a7c31600-d822-11eb-8553-8326da451e51.png)

 ![image](https://user-images.githubusercontent.com/69497292/123615207-b4e00500-d822-11eb-9527-3b157d9314fa.png)

 ![image](https://user-images.githubusercontent.com/69497292/123615282-c4f7e480-d822-11eb-8240-6cc1c5212f6f.png)

 ![image](https://user-images.githubusercontent.com/69497292/123615355-d80ab480-d822-11eb-9e57-eb1dda6d1091.png)

 ![image](https://user-images.githubusercontent.com/69497292/123615406-e658d080-d822-11eb-887b-4a2a5f98021d.png)
 
 ![image](https://user-images.githubusercontent.com/69497292/123615484-fa043700-d822-11eb-85e0-954e532d3c95.png)

 ![image](https://user-images.githubusercontent.com/69497292/123615748-39cb1e80-d823-11eb-8977-f6453272aa35.png)

 ![image](https://user-images.githubusercontent.com/69497292/123615847-50717580-d823-11eb-9a99-fc9f99c13af5.png)

 ![image](https://user-images.githubusercontent.com/69497292/123615907-5c5d3780-d823-11eb-890e-e12e920d0759.png)

 ![image](https://user-images.githubusercontent.com/69497292/123615941-6717cc80-d823-11eb-8751-4bb25e347bdb.png)

 ## DAY 5
 
 IF : Priority logic 
 if "if" condition is true it wont check front will come out of the loop
 
 case: It starts execution sequentially even if conditions are met, it will come out of the loop only after comparing all possible cases
 
 Caveats  with if:
 "If" can cause infered latches: Even if you dont intend to put latch. But because of bad coading style we get a latch:
 
 Some times we use this coading style also as our requirement. In comnbinational logic i should not have infered logic but sequential logic can have the latch according to requirement. But this should be a known thing, not to occur unknowingly

 Caveats with case:
 
 * Incomplete case will lead to inferred latches
 -  coading with default will avoid inferred latches
 * Partial assignment in case will also lead to inferred latches
 -  Even if we have default this will not resolve
 -  This can be resoved by assigning all the outputs in all the segment of case.
 * overlapping cases
 -  overlapping cases may result in unpredictable output it won't form latch

 ![image](https://user-images.githubusercontent.com/69497292/123621253-a399f700-d828-11eb-96e0-bd9525edd35d.png)

 ![image](https://user-images.githubusercontent.com/69497292/123621294-ae548c00-d828-11eb-8d94-c7ed4ffdc402.png)
 
 ![image](https://user-images.githubusercontent.com/69497292/123621368-c0362f00-d828-11eb-9917-b1482010b737.png)

 ![image](https://user-images.githubusercontent.com/69497292/123621435-d17f3b80-d828-11eb-86f6-c5b9f1ac278f.png)
 
 ![image](https://user-images.githubusercontent.com/69497292/123621485-e0fe8480-d828-11eb-95ac-9149b79bcb41.png)

 ![image](https://user-images.githubusercontent.com/69497292/123621534-f1166400-d828-11eb-9e00-0645b8d3d30c.png)

 ![image](https://user-images.githubusercontent.com/69497292/123621601-04c1ca80-d829-11eb-84cb-8953527e8c52.png)
 
 ![image](https://user-images.githubusercontent.com/69497292/123621678-1905c780-d829-11eb-9388-a8007c90c0c6.png)

 ![image](https://user-images.githubusercontent.com/69497292/123621829-3fc3fe00-d829-11eb-87d7-8b70dbb06d26.png)

 ![image](https://user-images.githubusercontent.com/69497292/123622179-929db580-d829-11eb-8e69-ec04594c6691.png)

 ![image](https://user-images.githubusercontent.com/69497292/123622331-b9f48280-d829-11eb-898e-8abbca48e9b4.png)

 ![image](https://user-images.githubusercontent.com/69497292/123622453-d98bab00-d829-11eb-8343-6bf946db7f6c.png)
 
 ![image](https://user-images.githubusercontent.com/69497292/123622591-05a72c00-d82a-11eb-8a43-3d3d6fa92cd8.png)

 
 ![image](https://user-images.githubusercontent.com/69497292/123622659-21123700-d82a-11eb-96ab-ba8fc35a94d4.png)

 ![image](https://user-images.githubusercontent.com/69497292/123622795-5028a880-d82a-11eb-81f1-279cf2dd4dd4.png)

 ![image](https://user-images.githubusercontent.com/69497292/123622874-69c9f000-d82a-11eb-8369-080660695324.png)
 
 ![image](https://user-images.githubusercontent.com/69497292/123622916-78b0a280-d82a-11eb-89e5-60026a63bf3c.png)

 ![image](https://user-images.githubusercontent.com/69497292/123622971-8b2adc00-d82a-11eb-9028-0256e7d1e8d9.png)
 
 ![image](https://user-images.githubusercontent.com/69497292/123623657-59fedb80-d82b-11eb-8a44-5851cbf2a710.png)

![image](https://user-images.githubusercontent.com/69497292/123623722-6b47e800-d82b-11eb-86d9-d114d73a5667.png)

 ![image](https://user-images.githubusercontent.com/69497292/123623819-84e92f80-d82b-11eb-9213-5b71771800ac.png)

 ![image](https://user-images.githubusercontent.com/69497292/123623910-9af6f000-d82b-11eb-9f83-4842c6781969.png)

 * Using looping constructs for hardware
 - For
 - Generate
 
 For : 
 * Is used inside always block.
 * Used to evaluate expression.
 * Finally using "for" inside always block will also lead to hardware. 


 
 
 
 






 

  

  
  
  

  
  
  
  
