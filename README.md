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

### Day 1- Inception of opensource EDA, OpenLane, and Sky130 PDK


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
  - Foundry IPs- Refers to the intellectual property blocks or design components that are provided by semiconductor foundries to their customers. These Foundry IPs are critical for chip designers, as they provide the basic building blocks necessary to create custom ICs .

</deatils>

<details>
<summary>RISC-V and software applications to hardware</summary>

![image](https://github.com/ani171/pes_pd/assets/97838595/e0a7a7fc-72cb-496d-94fb-c64c0f1be6be)
- HDL language acts a interface between the RISC architecture and the layout. It converts the RTL design into a netlist and synthesizes it.
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
