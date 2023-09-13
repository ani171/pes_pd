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
<summary> Introduction to QFN-48</summary>

- Quad Flat No-Lead 48, is a type of surface-mount integrated circuit package
-  It is characterized by having 48 pins arranged in a grid pattern around the perimeter of the package.
-  QFN packages are popular in electronics manufacturing due to their compact size, good thermal performance, and ease of assembly.
- Block diagram of a processor

![image](https://github.com/ani171/pes_pd/assets/97838595/effba290-e604-4f84-b915-e3d0036e359b)

1. SDRAM - Synchronous Dynamic Random-Access Memory (SDRAM) is a type of volatile semiconductor memory. ts primary function is to provide high-speed data storage and retrieval capabilities for temporary data storage and quick access by the processor
2. JTAG - Joint Test Action Group, is a standard interface and protocol used for testing and debugging integrated circuits, including chips and microcontrollers. The primary function of JTAG is to perform boundary scan testing. Boundary scan is a technique used to test the interconnections between the pins of an integrated circuit and detect faults or defects.
3. UART- Universal Asynchronous Receiver/Transmitter is a common serial communication interface.UART serves as a means for transmitting and receiving serial data between a chip and other external devices.
4. GPIO- General-Purpose Input/Output,is a versatile hardware that allows the chips to interact with the external world by providing the ability to read digital signals from external devices and send digital signals to external devices.
5. I2C- Inter-Integrated Circuit, is a serial communication protocol that is used to connect multiple digital devices together on the same bus.
6. QSPI- Quad Serial Peripheral Interface, is a high-speed serial communication protocol commonly used for data storage, memory access, and communication between microcontrollers, microprocessors, and external memory devices.It offers higher data transfer rates than traditional SPI's

- QNF-48
![image](https://github.com/ani171/pes_pd/assets/97838595/40d60952-0ea3-4153-a1d7-4a7e3f3667e4)
![image](https://github.com/ani171/pes_pd/assets/97838595/145f3ebc-2722-4dba-a02f-e326ab2cd333)
  - Pads -serve as the points of electrical contact between the IC within the package and the PCB on which the IC is mounted.
  - Core - The core of a QFN-48 package typically contains the integrated circuit (IC) itself, including the silicon die.
  - Silicon Die - This is where the actual circuitry, transistors, and electronic components are located. It's the functional core that processes data, performs computations, or manages various tasks based on the chip's design and purpose.
  - Wire Bonds - Silicon die is connected to the package's lead frame using fine wire bonds. These wire bonds provide electrical connections between the die and the external pins.
  - Macros - Predefined, reusable circuit elements or modules that are integrated into the overall chip design.
  - Foundary Ip's- Refers to the intellectual property blocks or design components that are provided by semiconductor foundries to their customers. These Foundry IPs are critical for chip designers, as they provide the basic building blocks necessary to create custom ICs .

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
