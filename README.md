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
<deatils>
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

</deatils>

<details>
<summary>RISC-V and software applications to hardware</summary>

![image](https://github.com/ani171/pes_pd/assets/97838595/e0a7a7fc-72cb-496d-94fb-c64c0f1be6be)
- HDL language acts an interface between the RISC architecture and the layout. It converts the RTL design into a netlist and synthesizes it.
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

`less floorplan.tcl`

![image](https://github.com/ani171/pes_pd/assets/97838595/db903803-925a-4c73-8d14-db665b461479)

`run_floorplan`

</details>
