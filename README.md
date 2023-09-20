# pes_pd

# Advanced Physical Design using openlane & sky130

<details>
<summary>Installation</summary>

- For windows
https://forgefunder.com/~kunal/openlane.zip
  - Download and extract the above zip file
  - Create a new machine on your Virtual box with Ubantu 19.04 Bionic Beaver Version
  - Add the extracted file into the machine
<br>
- Installation verification

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
```

![image](https://github.com/ani171/pes_pd/assets/97838595/ab9b061c-c35f-4864-a75a-627312965959)

</details>

## Day 1- Inception of opensource EDA, OpenLane, and Sky130 PDK

<details>
<summary>Introduction to QFN-48</summary>

- Quad Flat No-Lead 48, is a type of surface-mount integrated circuit package
-  It is characterized by having 48 pins arranged in a grid pattern around the perimeter of the package.
-  QFN packages are popular in electronics manufacturing due to their compact size, good thermal performance, and ease of assembly.
- Block diagram of a processor

![image](https://github.com/ani171/pes_pd/assets/97838595/effba290-e604-4f84-b915-e3d0036e359b)

1. SDRAM - Synchronous Dynamic Random-Access Memory (SDRAM) is a type of volatile semiconductor memory. Its primary function is to provide high-speed data storage and retrieval capabilities for temporary data storage and quick access by the processor
2. JTAG - Joint Test Action Group, is a standard interface and protocol used for testing and debugging integrated circuits, including chips and microcontrollers. The primary function of JTAG is to perform boundary scan testing. Boundary scan is a technique used to test the interconnections between the pins of an integrated circuit and detect faults or defects.
3. UART- Universal Asynchronous Receiver/Transmitter is a common serial communication interface.UART serves as a means for transmitting and receiving serial data between a chip and other external devices.
4. GPIO- General-Purpose Input/Output, is a versatile hardware that allows the chips to interact with the external world by providing the ability to read digital signals from external devices and send digital signals to external devices.
5. I2C- Inter-Integrated Circuit, is a serial communication protocol that is used to connect multiple digital devices together on the same bus.
6. QSPI- Quad Serial Peripheral Interface, is a high-speed serial communication protocol commonly used for data storage, memory access, and communication between microcontrollers, microprocessors, and external memory devices. It offers higher data transfer rates than traditional SPI's

- QNF-48
![image](https://github.com/ani171/pes_pd/assets/97838595/40d60952-0ea3-4153-a1d7-4a7e3f3667e4)
![image](https://github.com/ani171/pes_pd/assets/97838595/145f3ebc-2722-4dba-a02f-e326ab2cd333)
  - Pads -serve as the points of electrical contact between the IC within the package and the PCB on which the IC is mounted.
  - Core - The core of a QFN-48 package typically contains the integrated circuit (IC) itself, including the silicon die.
  - Silicon Die - This is where the actual circuitry, transistors, and electronic components are located. It's the functional core that processes data, performs computations, or manages various tasks based on the chip's design and purpose.
  - Wire Bonds - The silicon die is connected to the package's lead frame using fine wire bonds. These wire bonds provide electrical connections between the die and the external pins.
  - Macros - Predefined, reusable circuit elements or modules that are integrated into the overall chip design.
  - Foundry IPs- Refers to the intellectual property blocks or design components that are provided by semiconductor foundries to their customers. These Foundry IPs are critical for chip designers, as they provide the basic building blocks necessary to create custom ICs.

</details>

<details>
<summary>RISC-V and software applications to hardware</summary>

![image](https://github.com/ani171/pes_pd/assets/97838595/e0a7a7fc-72cb-496d-94fb-c64c0f1be6be)
- HDL language acts as an interface between the RISC architecture and the layout. It converts the RTL design into a netlist and synthesizes it.
![image](https://github.com/ani171/pes_pd/assets/97838595/7c0e4892-b24a-4548-8d45-546d34d40fb6)
Application software ---> System software ---> Hardware
- System Software converts application software into binary language
  - It has three major parts:
  1. Operating system
  2. Compiler
  3. Assembler
  - The operating system acts on small functions present in C, C++, Java, or any other language codes and gives it to the Compiler which in turn generates the .exe file which has all the Instructions. The .exe file is fed into the assembler, which generates the Machine Language code through which hardware can be implemented.
  
</details>

<details>
<summary>SoC Design and OpenLane</summary>

## Requirements for ASIC Design
![image](https://github.com/ani171/pes_pd/assets/97838595/667dc3c0-bd68-4eb3-9f53-5cb30a854fff)

 ## Simplified RTL to GDSII Flow
 ![image](https://github.com/ani171/pes_pd/assets/97838595/cf62946c-8489-4021-9644-968b320821b0)

- Synthesis: Synthesis in the context of ASIC (Application-Specific Integrated Circuit) design is a crucial step in the overall ASIC design flow. It involves converting a high-level hardware description language (HDL) representation of a digital design into a gate-level netlist, which consists of logical gates (AND, OR, XOR, etc.) and flip-flops (registers).
- Floor Planning: Floor planning is the process of determining how the various functional blocks, or modules, of an ASIC will be physically placed on the silicon die. It defines the overall chip's dimensions, the location of key components, and the routing channels for interconnects.
- Power planning: Power planning, also known as power grid design, is the process of distributing power and ground throughout the ASIC to ensure stable and efficient power delivery. It involves creating a network of power rails and ground connections.
<br>
- Global Placement:
    - Global placement is the initial phase of placement and focuses on finding a rough positioning of the cells on the chip's layout.
    - It does not specify the exact coordinates but rather provides a high-level allocation of resources.

- Detailed Placement:
    - Detailed placement follows global placement and focuses on refining the positions of individual cells to achieve precise spatial coordinates.
    - It determines the exact locations of each cell and ensures that cells are placed according to design constraints and the logical interconnections between them.
<br>
- Clock Tree Synthesis: CTS aims to efficiently distribute clock signals to all flip-flops and sequential elements in the design. This ensures that all clocked elements receive a synchronized clock signal, minimizing clock skew (the variation in arrival times of clock signals) and ensuring consistent operation.
- Signal Routing: This involves the process of connecting various electronic components and interconnecting the signal paths to ensure proper functionality.
- Global Routing
    - Global routing focuses on finding a rough path for each signal through the available routing channels to connect the source and destination points.
    - It doesn't specify the exact path of each wire but rather defines high-level routing structures.
- Detailed Routing
    - Detailed routing follows global routing and focuses on refining the exact paths of each signal.
    - It specifies the specific routing resources (metal layers, vias, etc.) to be used for each net and resolves conflicts.
<br>
- Sign-off:
  - Physical Rules Checking
      - Design Rules Checking
      - Layout v/s Schematic
  - Timing Verification
      - Static Timing Analysis

## Introduction to OpenLane

OpenLane is designed to democratize the ASIC design process by providing open-source tools and methodologies. It aims to reduce the barriers to entry and enable more people to design custom integrated circuits.
Clean means:
  - No LVS Violations
  - No DRC Violations
<br>
- striVe SoC family

![image](https://github.com/ani171/pes_pd/assets/97838595/9025acfa-77a6-464c-9eb7-e7007a1db4d2)

- OpenLane ASIC flow

![image](https://github.com/ani171/pes_pd/assets/97838595/3d60a6dc-7aea-41a4-81e1-bf8bf260b1dd)

- Design For Test (DFT)
  1. Scan Insertion
  2. Automatic Test Pattern Generation (ATPG)
  3. Test Patterns Compaction
  4. Fault Coverage
  5. Fault Simulation
  
### Physical Implementation

- Also called automated PnR (Place and Route)
  - Floor/Power Planning
  - End Decoupling Capacitors and Tap cell insertion
  - Placement: Global and Detailed
  - Post-placement optimization
  - Clock Tree Synthesis (CTS)
  - Routing: Global and Detailed
    
### Logic Equivalence clock

- Every time the netlist is modified, verification must be performed
  - CTS modifies the netlist
  - Post Placement optimizations modify the netlist
- LEC is used to formally confirm that the function did not change after modifying the netlist
### Dealing with Antenna rules violations

- When a metal wire segment is fabricated, it can act as an antenna.
  - Reactive ion etching causes charge to accumulate on the wire.
  - Transistor gates can be damaged during fabrication.
- Two solutions:
  - Bridging attaches a higher layer intermediary
    - Requires Router awareness 
  - Add antenna diode cell to leak away charges
    - Antenna diodes are provided by the SCL

</details>

<details>
<suumary>Open-Source EDA Tools</suumary>

### OpenLANE Directory structure detail

![image](https://github.com/ani171/pes_pd/assets/97838595/ed0e309b-bac7-4fea-8d30-54ab148bfa61)
![image](https://github.com/ani171/pes_pd/assets/97838595/6aee3f4c-3025-46a8-b4cf-7cec36196928)
![image](https://github.com/ani171/pes_pd/assets/97838595/29dc6214-6aab-4121-8133-6924b2020991)
![image](https://github.com/ani171/pes_pd/assets/97838595/73c2b12d-b4e7-4fd7-9a4b-adc9faa552e8)

- skywate-pdk : contains all pdk-related files.
- open_pdks: set of scripts and files that convert foundry level pdks to be compatible with open source PDA tools.
- sky130A: It is a variant of pdk.
- libs.tech: specific to technology
- libs.ref: specific to tools

### Design preparation steps

![image](https://github.com/ani171/pes_pd/assets/97838595/280bfdd2-6121-45df-b5e4-acccf8d49349)
![image](https://github.com/ani171/pes_pd/assets/97838595/6894d26d-ad90-47f0-82a3-e6d843132658)
![image](https://github.com/ani171/pes_pd/assets/97838595/7f075a34-00d7-48fa-86c0-6867e72a6f99)
`less config.tcl`
![image](https://github.com/ani171/pes_pd/assets/97838595/ab426974-ccd1-496a-9f65-ff709541d6b2)
`less sky130A_sky130_fd_sc_hd_config.tcl`
![image](https://github.com/ani171/pes_pd/assets/97838595/432832ec-0aa8-4b88-a22d-11ef3fa4c501)

### Design setup stage
![image](https://github.com/ani171/pes_pd/assets/97838595/38edc184-2e68-4673-a241-6ef04b2dd65f)

### Review files after design prep and run synthesis

 ```
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
run_floorplan
```
![image](https://github.com/ani171/pes_pd/assets/97838595/e7b10f56-ddfe-47b0-acee-f0245bcf0299)
![image](https://github.com/ani171/pes_pd/assets/97838595/12de6c12-2b2e-462b-88de-5fad6419886a)
`less merged.lef`
![image](https://github.com/ani171/pes_pd/assets/97838595/04525814-f1a8-4f5a-8477-86fa1a5716ac)
`less config.tcl`
![image](https://github.com/ani171/pes_pd/assets/97838595/59bf31a6-8b44-4001-b54c-01232623e3bc)

#### Results of synthesis

![image](https://github.com/ani171/pes_pd/assets/97838595/c3d967ba-29ce-462e-8f87-1b88ab9bc186)

1. Number of cells = 14876
2. Number of dff =1613
3. Flop Ratio = 0.108

`less picorv32a.synthesis.v`

![image](https://github.com/ani171/pes_pd/assets/97838595/fc78d558-ea4a-4420-9750-553a148d0bb2)

</details>

## Day 2 -  Good floorplan vs. bad floorplan and introduction to library cells

<details>
<summary>Chip floor planning considerations</summary>

- Utilization factor and aspect ratio
![image](https://github.com/ani171/pes_pd/assets/97838595/a963ec64-9426-47b0-8cef-01530124a27a)
  - Finding W and H
      - we begin with a simple netlist taking two D flip flips, aka launch flop, and the capture flop with a simple combinational logic between them.
        
![image](https://github.com/ani171/pes_pd/assets/97838595/b3492954-5341-4029-b374-9f014fea07fe)
Converting it into the physical dimension
![image](https://github.com/ani171/pes_pd/assets/97838595/cfcbdc66-b508-4366-8c63-bb94a3bbbc49)

Given the unit area for each logic gate, we implement this die multiple times on the silicon wafer to increase the throughput. When we implement the logic into the core, the logic cells occupy 100% of the core, thereby occupying 100% of the core.

![image](https://github.com/ani171/pes_pd/assets/97838595/20bd601a-f8d2-40e3-b27c-daac51e84282)

![image](https://github.com/ani171/pes_pd/assets/97838595/8090578f-5c86-48ea-91f4-e2280935c76e)

- Utilization factor:

![image](https://github.com/ani171/pes_pd/assets/97838595/f408c088-e3db-4aa9-a5c3-fc38e26b65f8)

- Aspect ratio:
  - Ratio of the width to the height of a transistor. It is a critical parameter in the design and fabrication of integrated circuits.
  - Whenever the aspect ratio is 1 it signifies that the chip is a square-shaped chip. When the aspect ratio is other than 1 then it signifies that our chip is rectangular in shape.

![image](https://github.com/ani171/pes_pd/assets/97838595/b17b1943-fbef-447f-9595-66540b0d60d1)

### Concept of pre-placed cells

![image](https://github.com/ani171/pes_pd/assets/97838595/48f7f577-07a2-459e-a359-aa184d29313f)

![image](https://github.com/ani171/pes_pd/assets/97838595/62ebe21d-7e52-4e7b-8a54-2de286c8e814)

- Separate the two blocks as two different IPs and modules.
- We can implement this one time and can be REUSED multiple times.

![image](https://github.com/ani171/pes_pd/assets/97838595/e8b11638-f660-4ef0-8f39-3fb075b880b4)

![image](https://github.com/ani171/pes_pd/assets/97838595/6d5349cf-22d7-4e56-8f9a-99194a898200)

### De-coupling capacitors

- Decoupling capacitors are a fundamental tool in ensuring the reliable and noise-free operation of digital circuits and ICs. Properly selected and placed decoupling capacitors can help prevent signal integrity issues, reduce electromagnetic interference (EMI), and improve the overall performance and reliability of electronic systems.

![image](https://github.com/ani171/pes_pd/assets/97838595/991c7dd4-f32c-4a2a-ac90-6377512c136f)

- If Vdd' goes below the noise margin, due to Rdd and Ldd, the logic '1' at the output of the circuit won't be detected as logic '1' at the input of the circuit following this circuit.

![image](https://github.com/ani171/pes_pd/assets/97838595/cfa63073-d0fc-47fd-b635-c5ff12f711b5)

- Having a large distance from the power supply and the main circuit has a disadvantage as there are multiple voltage drops happening before it reaches the main circuit giving less voltage at the main circuit due to voltage drops, therefore, we cannot guarantee that our logic gates in the circuit are getting either a high voltage(logic 1) or a low voltage(logic 0) or a danger region or gray region(Either Logic can go to 1 or 0 giving high or low volts) hence we have a disadvantage of Voltage being far from our circuit design.
- To solve this we use Decoupling Capacitors
  - they are huge capacitors completely filled with charge, therefore if our main voltage source is 1v our decoupling capacitors also get charged to 1V.

![image](https://github.com/ani171/pes_pd/assets/97838595/57b37281-1b88-403f-bbb0-de5fd6d0c9a6)

  - surround the preplaced cells with the decoupling capacitors in order to keep the current flow as required without any problems of voltage drops. thereby ensuring each preplaced cell is getting the supply from the Decoupling capacitors.

![image](https://github.com/ani171/pes_pd/assets/97838595/66a144fd-7318-41e3-a44c-dfe918cae1e1)

### Power planning

- Power planning involves the careful management of power distribution, delivery, and consumption in an IC to ensure its proper functioning and efficiency.

![image](https://github.com/ani171/pes_pd/assets/97838595/69d1559a-de19-4dde-83a0-acd94a4e391a)

- Consider the above circuit which we used for decoupling capacitors and converting it into a Macro, now This macro is repeated multiple times on the chip creating a current Demand for each and every element of the particular macro. Now suppose one is the driver and the other is the loader each macro has decoupling capacitors and we need to send the signal from the driver to the load, we need to make sure the particular line between the driver and to load maintains the same particular signal.

![image](https://github.com/ani171/pes_pd/assets/97838595/0736914d-c013-435d-96e7-db919f71e765)

- The line between the driver and load should get the necessary power from the power supply as decoupling capacitors cannot be placed in between therefore having a possibility of voltage drop as the power supply is far from the signal line.
- Hence we consider a 16-bit bus connected to an inverter when we pass the logic to the inverter the output will be the inverted value of the input therefore all the capacitors charged to Logic 1 are now discharged to Logic 0 and vise-versa.

![image](https://github.com/ani171/pes_pd/assets/97838595/33f2ab90-1098-4eef-8a7c-b2c45bda1778)

![image](https://github.com/ani171/pes_pd/assets/97838595/2453ebcd-a460-47cc-9c02-3a4196f483f9)

- when all the other capacitors charge from Logic 0 to Logic 1 in that case all these capacitors are in demand supply from the main power supply at the same time and we have a single voltage line for all the capacitors hence we get a Voltage Droop


![image](https://github.com/ani171/pes_pd/assets/97838595/3f5610e6-7ed6-4ca3-952c-531f30b6ac92)

- We put multiple power supplies instead of a single one by creating multiple VDD and VSS lines, thereby giving any power supply demand to the circuit. The power planning structure

### Pin placement and logical cell placement blockage

- Pin placement, also known as I/O (Input/Output) pad placement, refers to the process of determining the locations and arrangement of input and output pins on an IC or PCB. These pins are used to interface with external devices or other components.

![image](https://github.com/ani171/pes_pd/assets/97838595/51ba5ec5-dae0-4a72-837a-6833d64aa619)

- Let's take 2 more designs but both are driven using different clocks with a common pre-placed cell as shown below:

![image](https://github.com/ani171/pes_pd/assets/97838595/73ec9440-0cfc-43c6-8be6-9282fec5d44c)

- Complete Design

![image](https://github.com/ani171/pes_pd/assets/97838595/5be8efa4-99a1-4058-9df7-4b0db478dbe0)

- Clock 1 and 2 drives the complete chip

### Pin placement

![image](https://github.com/ani171/pes_pd/assets/97838595/835166ab-5fee-4a50-b704-5655386dfe9f)

- After Pin placement, we make sure that none of the automated placement and routing tools place any cells in the particular area that the gaps between each clock port, the area should be blocked for placement and routing tools, hence we do logical cell placement blockage.

![image](https://github.com/ani171/pes_pd/assets/97838595/5b6b0e64-6eb3-4b04-82e0-fba2698825ad)

### Steps to run floorplan using OpenLANE

`less README.md`

![image](https://github.com/ani171/pes_pd/assets/97838595/779e9791-7eca-4f19-ab3b-0883387c7492)
![image](https://github.com/ani171/pes_pd/assets/97838595/508c7a63-f3e2-4f10-b8c4-ba26e83600fb)
![image](https://github.com/ani171/pes_pd/assets/97838595/814c5f45-93af-4023-b079-d22399ba42cc)

`less floorplan. tcl`

![image](https://github.com/ani171/pes_pd/assets/97838595/db903803-925a-4c73-8d14-db665b461479)

`run_floorplan`

![image](https://github.com/ani171/pes_pd/assets/97838595/218fda9b-7838-4c49-9a23-17de9d466730)

### Review floorplan layout in Magic

```
magic -T /home/nickson/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged. lef def read picorv32a.floorplan.def &
```

![image](https://github.com/ani171/pes_pd/assets/97838595/9044feaa-e94c-414f-86b4-802fb460c7a6)

- Click "S" to select the layout
- Click "V" so that the layout will fit the screen

![image](https://github.com/ani171/pes_pd/assets/97838595/07badb76-347c-4186-9aa7-e839913a6847)
![image](https://github.com/ani171/pes_pd/assets/97838595/5bf4949d-4416-4eb3-b1d5-4ddc071f8080)
![image](https://github.com/ani171/pes_pd/assets/97838595/2071fac3-c677-4625-99ab-9d507fa04316)

</details>

<details>
<summary>Library Binding and Placement</summary>

### Netlist binding

- Placement and Routing
  - The most important step in placement and routing is to bind the netlist with the physical cells.
  - Consider the particular netlist with all these Gates and the shape of the gates represents the functionality of the Gates, but in reality, we don't have shapes like the ones shown below we have them in box type with the width and height of the particular cell.
  - So at the end, we will be having each logic gate with a shape and the preplaced blocks and we will be left out with wires.

![image](https://github.com/ani171/pes_pd/assets/97838595/fa4225f6-3f93-456b-9d4e-22e6c3e10061)

  - These blocks of shape are now present on a shelf known as the Library, The Library contains various types of blocks including these(ex flip flops, AND gate, Or gate, etc)

![image](https://github.com/ani171/pes_pd/assets/97838595/25de1a1f-5821-4362-b7a1-13d3e138dc39)

  - The library also holds the information of each logic gate like delays etc, the library can be classified into 2 types one that holds the shapes and one that holds the information of each logic gate.
  - The library will have the information on the shape width and height, the delay information of each and every cell, and the required condition of the particular cells.
  - The library also holds different flavors of the cell it tries to store(ex if the 2 block is an and gate the library also shows another same AND gate but a bit bigger in size, least resistance path than the normal one as its bigger in size thereby being faster compared to the normal one), therefore it has flavors of each and every cell we try to store it in.

![image](https://github.com/ani171/pes_pd/assets/97838595/8390e6e2-e257-48a0-8a2f-29b6d17afe3a)

  - we can pick what we want to use based on our available space on the floorplan.
  - Therefore in summary library consists of everything it consists of cells, shapes and sizes of the cells, various flavors of the same cells, and the timing and delay information.

- Once we have given proper shape and size and delay information of our cell using the library the next step is to take this cell and place it onto the floorplan, so we have the floorplan, we have the netlist, we have the physical design view of the netlist in form of logic gates.

![image](https://github.com/ani171/pes_pd/assets/97838595/21e7a196-ed5c-4c4c-adb6-6b254b9fdfa3)

- The netlist won't come into the picture as we will be using the Physical view of logic gates though we will be following the connectivity information from the netlist itself.

- How this is done?
  - The placement stage will make sure that the pre-placed cell locations are not affected and kept as it is and there will be no cells that can be placed in that area.
  - We now place each of the shape cells from the physical design view of logic gates in a proper manner such that there are no delay constraints, we place them in such a way that they are close to their respective input and output port pins, and we place them close because if FF2 was placed somewhere below and the distance from FF2 to dout1 wud be higher thereby having more timing delay to communicate with the output pin.

![image](https://github.com/ani171/pes_pd/assets/97838595/7cf8f142-03c3-4093-86cf-f0d4bef124d4)

- From above we clearly see that FF1 is placed near to Din1 and FF2 is placed near to Dout1 as they are connected close to each other using the Netlist as reference we fill all the other the same way.
- we place the 2nd stage of the netlist in the way shown below:

![image](https://github.com/ani171/pes_pd/assets/97838595/299bade4-29ec-41ec-b95c-7e2fdbefb850)

- Here we see that in 2nd stage FF1 is not close to Din2 for and FF1, cell 1, cell 2, FF2 the delay between FF1 and 1 will be very minimal and similarly the delay between 1 and 2 is also minimal, we do this because of some reasons given ahead.

### Optimize placement using estimated wire length and capacitance

- In the 3rd stage placed we see that FF1 needs to be connected to Din3 and FF2 to Dout 3 but the distance between them is huge hence we try to place them diagonally as shown below:
![image](https://github.com/ani171/pes_pd/assets/97838595/f7f7dc15-e8e7-4933-884c-ed507ca06010)

- Similarly implementing stage 4 is quite tricky as we have pre-placed cells and we can't give FF1 close to Din4 therefore the distance is huge again in stage 4 as there is again a diagonally opposite I/O port for stage 4 on the chip.
- We place the stage as shown below:
![image](https://github.com/ani171/pes_pd/assets/97838595/61ce154e-2970-41a6-a272-f944b8b6cc69)
- Now we try to solve the problems that we encountered while placing these cells, the Solution for these problems is known as Optimized placement.

  - This is the stage where we do estimations where we estimate the wire length, and capacitance and based on that insert repeaters.
   - Let's consider FF1 of the 2nd stage and din2 we see that the capacitances between them are very huge as its huge length of wire and even the resistance as it depends on the length and length is huge. Therefore the signal delay is high from din2 to FF1 of 2nd stage due to the distance.
  - We fix this problem by placing a Repeater in between Din2 and FF1 of the 2nd stage to pass on the signal thereby reducing delay and loss of data, therefore whatever is told to Din2 is successfully retained by FF1 of the 2nd stage This is called Signal Integrity.
<br>

- Repeater: Repeats act as signal buffers that rejuvenate the existing signal, generating a new signal identical to the original one, and transmitting it once more. This strategy involves deploying multiple repeaters to preserve signal quality over extended distances, albeit at the expense of increased area usage, presenting a trade-off.
- In the 1st stage we don't need any repeaters, Signel Integrity is based on the wire length estimation and calculation.
- SLEW primarily relies on the capacitor's value; a larger capacitor necessitates a greater charge to fill it, leading to a poorer slew rate. In the second stage, a considerable distance separated Din2 and FF1 from Stage 2, causing the slew rate, which essentially involves transmission, to exceed its limit. This increased difficulty in reaching FF1 necessitates the addition of repeaters, as illustrated below

![image](https://github.com/ani171/pes_pd/assets/97838595/e6fce526-9731-4cdc-b3b7-0bbe4016ed03)

- In the second stage, we have optimized specific logic to eliminate any time delay between components 1 and 2, ensuring seamless signal recreation, as they are all closely positioned. The rationale behind this optimization for FF1, 1, 2, and FF2 of the second stage is our assumption that this stage operates at an exceptionally high speed. Consequently, we have clustered these logic elements in close proximity to achieve a zero-delay transmission from FF1 to FF2, even though they are distanced from their respective ports
- Stage 3
![image](https://github.com/ani171/pes_pd/assets/97838595/289d992c-1a2f-4c28-9066-94d2da97c03c)

- Stage 4

![image](https://github.com/ani171/pes_pd/assets/97838595/cbdcd049-da3c-4ff4-99e5-8935c8df9b12)

### Need for libraries and characterization

Libraries and characterization are foundational elements of the IC design process. Libraries provide standardized building blocks that enhance design productivity and reusability, while characterization provides the essential data needed to accurately model and simulate the behavior of these components, ensuring that the final design meets its performance, power, and reliability goals.

### Congestion-aware placement using RePlAce

Placement within OpenLANE involves a two-stage process:
1. Global Placement: This initial stage focuses on placing the cores without performing legalization. Legalization involves arranging standard cells in standard cell rows, ensuring they are properly abutted with one another, and avoiding any overlaps. The primary goal of global placement is to minimize wire length.
2. Detailed Placement: This phase can be rephrased as "Detailed placement" occurs after global placement. In this stage, the focus shifts to fine-tuning the placement of standard cells and ensuring all legalization requirements are met. The primary aim here is to optimize the precise arrangement of cells to further enhance circuit performance.

- For global placement, we run the `run_placement` command
![image](https://github.com/ani171/pes_pd/assets/97838595/70f34a8a-97bb-4a28-a628-eeb3cd76cbb0)

- We see that the hpwl values converge basically the length is reducing.
- To see the placement in OpenLANE type magic -T with the required file location of the placement file.
![image](https://github.com/ani171/pes_pd/assets/97838595/6f598cb0-ce44-446d-b16a-ce0c0544d283)
![image](https://github.com/ani171/pes_pd/assets/97838595/5fb9e674-cffe-41a3-a7bf-8abbd7eaf5f6)

</details>

<details>
<summary>Cell design and characterization flows</summary>

### Inputs for cell design flow

- The cell design flow involves the systematic creation and enhancement of discrete digital logic cells that constitute a standard cell library. Within these libraries, there exists a collection of pre-designed, characterized, and recyclable components, such as logic gates and flip-flops, fundamental for building integrated circuits. These libraries encompass various essential elements, including PDK, DRC, and LVS rules, SPICE models, as well as user-defined specifications. These user-defined specifications, such as pin placement and gate length parameters, are incorporated into the library by the library developer.
![image](https://github.com/ani171/pes_pd/assets/97838595/28ef7c44-3535-46f7-a45b-3f99c5f3f5a8)
![image](https://github.com/ani171/pes_pd/assets/97838595/be1e9c0e-feff-4110-8e49-5f6ed92008ac)

### Circuit Design

- Circuit Design Phase: In this initial phase, we begin by implementing a specific function using a combination of NMOS (N-type Metal-Oxide-Semiconductor) and PMOS (P-type Metal-Oxide-Semiconductor) transistors. Subsequently, we create a network graph that represents the interconnections between these transistors. From this graph, we derive Euler's path, which serves as a crucial aspect of the design. Additionally, we construct a stick diagram that visually represents the physical layout of the circuit based on the graph.
![image](https://github.com/ani171/pes_pd/assets/97838595/668f9253-50d7-4ab0-9c1d-0dc5fe59353e)

- Layout Design Phase: Following the stick diagram, we proceed with the layout design, adhering to Design Rule Check (DRC) rules to ensure manufacturability. This phase involves accurately converting the stick diagram into a layout that meets the specified DRC constraints. Furthermore, we extract parasitic elements, such as resistances and capacitances, from the layout. This information is then compiled into an extracted spice list.
![image](https://github.com/ani171/pes_pd/assets/97838595/5f88c636-0802-40f7-af0e-6126dbcfb546)
![image](https://github.com/ani171/pes_pd/assets/97838595/51e5811f-39af-4b3c-9118-2d7356573c01)

- Characterization Phase: In this step, we focus on characterizing the circuit's performance in terms of timing, noise, and power. We begin by importing the necessary models and technology files. Using this information, we generate an extracted spice netlist that reflects the circuit's behavior. Subsequently, we read subcircuits and integrated power sources into the design. We also apply a stimulus to the characterization setup, introduce required output capacitance loads, and provide the essential simulation commands to thoroughly evaluate the circuit's behavior under various conditions.
![image](https://github.com/ani171/pes_pd/assets/97838595/4a2c4af9-4a7f-4667-9703-09179ae4ca74)

This process involves transitioning from the initial logical representation of the circuit to its physical layout, ensuring adherence to design rules, extracting parasitic effects, and ultimately characterizing its performance through simulation and analysis.
- We have the description of this buffer as shown below:
![image](https://github.com/ani171/pes_pd/assets/97838595/b2490d1e-9190-443b-bb6a-c3bd093f25eb)

- For this, we have spice extracted Netlist basically whatever we have in the Layout buffer that contacts the metal layers, and everything for each element will have a resistance and capacitances we have extracted them all in terms of a spiced Netlist as shown below:
![image](https://github.com/ani171/pes_pd/assets/97838595/1be3c9ff-c613-4763-a08c-59ba00559250)

- We have the sub-circuit file loaded, it contains the actual PMOS and NMOS models as shown below:
![image](https://github.com/ani171/pes_pd/assets/97838595/581fcb78-4102-43e1-a0ef-2a26d4b9f99e)

- The industry-standard characterization flow comprises several key steps
1. Model Reading: The initial step involves reading the models, which are the first files received from the foundry.
2. Extracted Spice Netlist Reading: Next, we read the extracted spice netlist, which provides an essential representation of the circuit.
3. Behavior Recognition: In this stage, we identify and characterize the behavior of the buffer or logic gate that has been implemented.
4. Loaded Subcircuit File Reading: We proceed by reading the loaded subcircuit file to integrate the necessary components.
5. Power Source Attachment: Essential power sources are attached to the circuit to ensure proper operation.
6. Stimulus Application: Stimulus is applied to initiate and observe the circuit's response.
7. Output Capacitance Variation: Output capacitance is adjusted within a specified range to assess circuit performance under different conditions.
8. Simulation Commands: Crucial simulation commands are provided to simulate and evaluate the circuit.
- These eight steps are typically consolidated into a configuration file that is input into the characterization software, known as GUNA. GUNA performs comprehensive characterization, generating separate timing, power, noise, and .lib (library) files. As a result, characterization is further subdivided into timing, power, and noise characterization processes.

</details>

<details>
<summary>General timing characterization parameters</summary>
  
- By examining the descriptive image of the buffer during characterization, we gain insights into various threshold points within the waveform. These points are referred to as "Timing Threshold Definitions." Below, you can find the timing thresholds for the depicted image.
- The output of the waveform looks like this shown below:
  
![image](https://github.com/ani171/pes_pd/assets/97838595/c59122ae-54ae-4352-94b4-d20560d13572)

- The waveform presented above is designed to provide insights into the slew rates of the signal. The red graph represents the rising slew, while the blue graph illustrates the falling slew, with distinct high and low values for each. Additionally, similar representations are available for input rise and fall as well as output rise and fall, with the input rise and fall depicted below.

![image](https://github.com/ani171/pes_pd/assets/97838595/587ed7c7-3982-4bd8-aa90-418583f675cf)

- The output rise and fall is shown below:
![image](https://github.com/ani171/pes_pd/assets/97838595/3865300c-c92a-460d-9063-2d70a2d6a4fb)

- Timing threshold definitions

![image](https://github.com/ani171/pes_pd/assets/97838595/ffbbe4be-4138-40a7-8fba-d40cb45d9405)

- Propagation delay: The time difference between when the transitional input reaches 50% of its final value and when the output reaches 50% of its final value.
```
Propagation delay=time(out_fall_thr)-time(in_rise_thr)
```
![image](https://github.com/ani171/pes_pd/assets/97838595/afe8aa07-d711-4422-a60d-0a58f4db33c7)
![image](https://github.com/ani171/pes_pd/assets/97838595/ade0f4eb-d796-4405-94cc-9ef8a12eed0a)

- Transition Time: The time it takes the signal to move between states is the transition time, where the time is measured between 10% and 90% or 20% to 80% of the signal levels.
```
Rise transition time = time(slew_high_rise_thr) - time (slew_low_rise_thr)
```
```
Fall transition time = time(slew_high_fall_thr) - time (slew_low_fall_thr)
```
![image](https://github.com/ani171/pes_pd/assets/97838595/cb5f8e16-e0f0-476a-a6c6-f20e5094b87f)

</details>

## Day 3 - Design library cell using Magic Layout and ngspice characterization

<details>
<summary>Labs for CMOS inverter ngspice simulations</summary>

- The IO Placer revision process in Place and Route (PnR) is an iterative workflow, allowing for adjustments to environment variables as needed. One example is the flexibility to modify the pin configuration within the core area, transitioning from an initially evenly distributed placement to an alternative arrangement when necessary.
![image](https://github.com/ani171/pes_pd/assets/97838595/80426bdf-8c04-4fe3-b43e-93bdabbeab56)
- Here in the above image we see that all the I/O pins are located at output equidistant of each other.
- to view the floorplan mode we can go to `floorplan.tcl`
![image](https://github.com/ani171/pes_pd/assets/97838595/9465ae6a-b61f-489a-b72f-ca078c7e2cf7)

- After making modifications to the run floorplan by changing the mode to 2, the resulting layout features a structure in which the I/O pins are positioned in a stacked configuration, meaning they are arranged vertically, with one pin directly above another. This stacking arrangement can be useful for optimizing space utilization and improving signal routing efficiency in the design.

![image](https://github.com/ani171/pes_pd/assets/97838595/0e024cb4-1a88-4ae1-a83d-f86f987b9e79)

### Lab steps to git clone vsdstdcelldesign

- During this lab session, our task involves utilizing Git to clone document files associated with PMOS and NMOS spice models. Subsequently, upon performing the Git clone operation, a VSD standard cell design file will be generated within OpenLane.
- Cloning repository
```
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```
![image](https://github.com/ani171/pes_pd/assets/97838595/0e0352f1-d80c-4768-b32f-9940c4649030)

- To obtain the layout
```
magic -T sky130A.tech sky130_inv.mag &
```
![image](https://github.com/ani171/pes_pd/assets/97838595/647c5c12-45d0-4a09-b588-e4482a5666b7)

</details>

<details>
<summary>Inception of Layout A CMOS fabrication process</summary>

### Lab introduction to Sky130 basic layers layout and LEF using inverter

![image](https://github.com/ani171/pes_pd/assets/97838595/647c5c12-45d0-4a09-b588-e4482a5666b7)

- In the depicted image, we are observing the result of running an inverter design in the "magic" software. This inverter includes both PMOS and NMOS transistors with their respective source and drain connections.
- The colors used in the image, such as red, blue, and green, serve as standard indications for different materials like polysilicon and metal. Each color corresponds to a specific metal layer.
- It's important to note that what we see in the image represents the physical layout design of the circuit, which is created following specific design rules. These design rules are crucial for ensuring the accuracy and functionality of the layout.
- The image effectively illustrates how the connections between the PMOS and NMOS transistors are established, including their drain and source connections.
- Furthermore, the layout design reflects the meticulous adherence to various layers and design rules that are fundamental in the precise construction of the circuit. This adherence ensures that the circuit functions as intended while meeting manufacturing and electrical requirements.

### Lab steps to create std cell layout and extract spice netlist
```
pwd
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```

![image](https://github.com/ani171/pes_pd/assets/97838595/b63823c8-1970-467e-a4ee-2adb9add1d96)

- DRC Errors
  - DRC Errors are issues or violations that occur during the Design Rule Check (DRC) phase in semiconductor design.
  - These errors indicate instances where the physical layout of a semiconductor device or integrated circuit does not conform to the specified design rules, which are essential for ensuring manufacturability and functionality.
  - DRC errors must be identified and rectified to produce a design that can be successfully manufactured and operated as intended.

![image](https://github.com/ani171/pes_pd/assets/97838595/8b29961e-4704-4f82-8760-dabcdd1bbf7e)

- SPICE File

![image](https://github.com/ani171/pes_pd/assets/97838595/01b7601c-3b4a-4c34-a323-87a57fbea9fc)

</details>

<details>
<summary>Sky130 Tech File Labs</summary>

### Lab steps to create the final SPICE deck using Sky130 tech

![image](https://github.com/ani171/pes_pd/assets/97838595/e2b7d6e4-02b6-4335-9b19-89c84c418cfc)

- ngspice
![image](https://github.com/ani171/pes_pd/assets/97838595/714f4e74-8efa-4df8-aeb5-3f5bd64e3dc6)

- To get the plot
`plot y vs time a`
![image](https://github.com/ani171/pes_pd/assets/97838595/beaae377-8f19-4393-929c-e03fbd088cd9)

### Introduction to Magic tool options and DRC rules

- Magic, a VLSI layout tool, originated in the 1980s at Berkeley under the development of John Ousterhout, who later gained recognition for creating the Tcl scripting language. Its continued popularity among universities and small companies can be attributed, in part, to its open-source Berkeley license. This licensing approach has enabled VLSI engineers with programming skills to introduce innovative ideas and keep magic aligned with the latest fabrication technology.
- However, what truly sets magic apart and contributes significantly to its popularity are its well-crafted core algorithms. Magic is often lauded as the most user-friendly option for circuit layout, even by those who primarily use commercial tools in their product design workflows.
- To download the required tech files
```
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
```

![image](https://github.com/ani171/pes_pd/assets/97838595/62924f00-61a8-476d-8187-5535cc9b39cb)

- Command to open magic

```
magic -d XR
```
![image](https://github.com/ani171/pes_pd/assets/97838595/22f59c74-df7a-459d-a3f3-81c76d5849ac)

- Opening the met3.mag file
![image](https://github.com/ani171/pes_pd/assets/97838595/0e684d7c-3e50-40ec-b1ed-94bcc0f7e517)

- for contact cuts, using the command `cif see VIA2`, we get
![image](https://github.com/ani171/pes_pd/assets/97838595/c855e390-b6c1-4f89-be6e-5ffd16a092ef)

### Fixing errors
- To find errors: Using the mouse select the area in b/w the ploy layers. Use the box command to get the measurement
![image](https://github.com/ani171/pes_pd/assets/97838595/1c1b469f-0dfa-43f5-8b52-ad3341721b86)
![image](https://github.com/ani171/pes_pd/assets/97838595/7fece0aa-5e33-4ee7-bd01-5aed146fadcc)

- To fix the error open the sky130A.tech file using an editor and search for poly.9 and make the changes
![image](https://github.com/ani171/pes_pd/assets/97838595/c2df35a9-c606-4d75-a77f-77cf9e25a6f7)

![image](https://github.com/ani171/pes_pd/assets/97838595/0a448e7d-ff2d-4594-a971-00739a2a7325)

- DRC Check
![image](https://github.com/ani171/pes_pd/assets/97838595/c4637b05-11fd-4bec-9264-19a733f45540)

### Lab exercise to describe DRC error as a geometrical construct

![image](https://github.com/ani171/pes_pd/assets/97838595/7346d3a7-0283-4c5f-abbe-3d0e7604dbba)

- Type in the following commands in the .main file
```
cif ostyle drc
cif see dnwell_shrink
cif see dnwell_missing
```
![image](https://github.com/ani171/pes_pd/assets/97838595/495e8beb-5ecf-4053-ab11-d28036ca87b6)
![image](https://github.com/ani171/pes_pd/assets/97838595/501681d9-80f5-42f0-99b6-782b00957b77)

</details>

## Day 4- Pre-layout timing analysis and importance of good clock tree

<details>
<summary>Timing Modelling using Delay Tables</summary>

- In the realm of Place and Route (PnR) activities, we rely on an abstract representation of GDS files produced through Magic. This abstract view, which is formally defined as LEF (Library Exchange Format) information, serves as a critical resource for interconnect routing during PnR.
- From the perspective of PnR, specific guidelines must be adhered to in order to establish a standard cell set:
  1. Port Placement: The input and output ports must be strategically positioned at the intersection points of vertical and horizontal tracks. This precise placement ensures efficient connectivity between components within the layout.
  2. Cell Dimensions: The dimensions of standard cells need to align with certain principles. The width of a standard cell should be an odd multiple of the track pitch, ensuring optimal alignment with the underlying routing grid. Similarly, the cell's height should adhere to odd multiples of the vertical track pitch, promoting congruence with the grid structure.

### To convert grid info to track info

- Go the the following path
```
Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130fd_sc_hd
```
![image](https://github.com/ani171/pes_pd/assets/97838595/c1a74208-320d-45e6-9abc-e3f938eadaa2)

- to use Grid commands type `grid` in tkcon
- Type the values of x and y
![image](https://github.com/ani171/pes_pd/assets/97838595/7ba61730-cc83-4b7d-8c6f-e0ac32858a95)
![image](https://github.com/ani171/pes_pd/assets/97838595/96987fc5-3a07-49bc-b573-44a26fdf4957)

- 1st numeric column indicates the offset and 2nd indicates the pitch along a provided direction

![image](https://github.com/ani171/pes_pd/assets/97838595/35bc3bf1-2e9c-4fb8-b948-0303ef91c6f1)

![image](https://github.com/ani171/pes_pd/assets/97838595/e580b5d5-d9cf-415c-9d85-097df1be7c65)

### To convert magic layout to std cell LEF

- To save the modified layout from Magic
```
save sky130_vsdinv.mag
```
![image](https://github.com/ani171/pes_pd/assets/97838595/d175bdc5-7c7d-416d-8709-41c5869e69c2)

- To generate the LEF file
```
magic -T sky130A.tech sky130_vsdinv.mag
lef write
```
![image](https://github.com/ani171/pes_pd/assets/97838595/1885a710-5410-4b8e-840a-f8032bc5d654)

### Timing libs and steps to include new cells in the synthesis

- We copy the lef file created and the sky130 library to the src folder of the picorv32a folder.
```
cp sky130_vsdinv.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32/src
```
- Modify the config file to include the libraries and lef file
```
vim config.tcl
```
![image](https://github.com/ani171/pes_pd/assets/97838595/253c03d9-2230-47f1-904f-d766691da6b1)

- In OpenLANE we retrieve the 0.9 package.
```
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a -tag 17-09_18-21 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```
<img width="588" alt="1" src="https://github.com/ani171/pes_pd/assets/97838595/f1a33f21-25cc-4084-b983-a61233de4cbd">


</details>

<details>
<summary>Delay tables and timing analysis with ideal clocks using openSTA</summary>

- Delay tables, commonly known as delay models or delay tables, are vital components in the domain of digital circuit design and analysis. They provide a structured framework for representing and comprehending the intricacies of how signals propagate through logic gates and interconnections within a digital integrated circuit (IC). These tables capture essential information about the time it takes for signals to traverse various circuit components, which is crucial for ensuring that the circuit meets its stringent timing requirements.
-  Delay tables are instrumental in determining key parameters like setup and hold times. 
- The primary purposes of delay tables are as follows:
  - Timing Analysis: They are essential for performing timing analysis, ensuring that signals meet their timing constraints, and identifying potential violations.
  - Synchronization: They help in synchronizing different parts of a digital system to ensure that data is sampled or latched correctly.
  - Power Estimation: Delay tables are used for estimating power consumption in digital circuits since power dissipation is directly related to signal transitions.
-  Delay tables typically include the following components:
  1. Input Conditions: These conditions specify the input signal values or transitions that trigger the delay calculation. Inputs can include input signal values, load conditions, and transition times.
  2. Gate Delays: Delay tables include information about the propagation delays of various logic gates, such as AND, OR, NAND, NOR, XOR, and others. These delays depend on the gate's technology, fan-out, and input conditions.
  3. Interconnect Delays: They account for the delays introduced by the wires and routing between logic gates. Interconnect delays depend on the physical characteristics of the wires, including length, resistance, and capacitance.
  4. Output Loads: The output load conditions specify the capacitive load that the gate must drive, which affects the output delay.

### Lab steps to configure synthesis settings to fix slack and include vsdinv

- Setup Timing Analysis: Setup timing analysis is a critical aspect of digital circuit design and verification. It focuses on ensuring that data signals meet the required setup time constraints at the inputs of sequential elements (e.g., flip-flops) in a digital system. The primary goal of setup timing analysis is to ensure that data is stable and valid before it is clocked into a flip-flop or other storage elements.
- Flip-flop setup time: The setup time (Ts) for a flip-flop is a critical parameter that determines when a data input signal must be stable before the arrival of the clock edge to guarantee proper data capture. It is defined as the minimum amount of time the data input must be held at a valid logic level before the active clock edge (e.g., rising edge) for reliable storage.

![2](https://github.com/ani171/pes_pd/assets/97838595/bd63529b-1b24-4472-a5b3-3d60898a577d)

### Clock Jitters and Uncertainty
- Clock Jitter
  - Clock jitter pertains to the transient irregularities or oscillations observed in the timing of a clock signal's edges.
  - This parameter holds significant importance in digital and communication systems due to its potential impact on overall system performance, particularly in high-speed or sensitive contexts.
  - Clock jitter can be attributed to diverse factors and may manifest as either random or deterministic variations in the timing of the clock signal.

- Clock Uncertainty
  - Clock uncertainty, alternatively known as clock skew, deals with the discrepancies in the arrival times of clock signals at various locations within a digital system.
  - Unlike clock jitter, which focuses on short-term variations, clock uncertainty primarily concerns long-term timing inconsistencies.
  - This phenomenon has the potential to significantly influence system performance and timing accuracy, making it a crucial consideration in digital design.
  - Clock uncertainty stems from various factors, including delays within the clock distribution network, routing delays, and variations in the lengths of clock paths.
  - These variations in clock arrival times can lead to synchronization challenges and may require mitigation strategies to ensure reliable system operation.

</details>

<details>
<summary>Clock tree synthesis TritonCTS and signal integrity</summary>

- OpenSTA, an open-source static timing analysis tool, is a widely employed resource in the realm of digital circuit design.
  - Static Timing Analysis (STA) is a pivotal phase in the design and validation of digital circuits, serving to verify that the circuit complies with its stringent timing constraints.
  - OpenSTA plays a significant role within the comprehensive OpenROAD open-source RTL-to-GDSII flow, constituting a vital component of this complete ASIC (Application-Specific Integrated Circuit) design environment.

```
read_lef /openLANE_flow/designs/picorv32a/runs/18-09_06-26/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/18-09_06-26/results/cts/picorv32a.cts.def
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/18-09_06-26/results/synthesis/picorv32a.synthesis_cts.v
read_liberty -max $::env(LIB_SLOWEST)
read_liberty -max $::env(LIB_FASTEST)
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```
![image](https://github.com/ani171/pes_pd/assets/97838595/b861059b-647d-4a16-be5e-d94a8d546741)

</details>

<details>

  <summary> DAY 5 </summary>

## Power Distribution Network
After generating our clock tree network and verifying post routing STA checks we are ready to generate the power distribution network **gen_pdn** in OpenLANE. The PDN feature within OpenLANE will create the following - power ring global to the entire core, power halo local to any preplaced cells, power straps to bring power into the center of the chip and power rails for the standard cells.

It is important to note that the pitch of the metal 1 power rails defines the height of the standard cells.

## Global and Detailed Routing
OpenLANE uses TritonRoute as the routing engine. We use **run_routing** to get the routed design. 

There are 2 stages in routing - global and detailed. Global routing first partitions the chip into routing regions and searches for region-to-region paths for all signal nets. This is followed by detailed routing, which determines the exact tracks and vias of these nets based on their region assignments.

If DRC errors persist after routing, we have 2 options - re-run the routing or manually fix the DRC errors.

## SPEF Extraction
Once the routing process is finished, you can proceed to extract interconnect parasitics for conducting sign-off post-route STA (Static Timing Analysis). These parasitics are extracted and stored in a SPEF (Standard Parasitic Exchange Format) file. It's important to note that the SPEF extraction tool is currently not integrated into OpenLANE.
Use the following commands for SPEF extraction.
```
cd ~/Desktop/work/tools/SPEFEXTRACTOR
python3 main.py <path to merged.lef in tmp> <path to def in routing>
```

</details>
