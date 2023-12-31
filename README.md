# Advanced_Physical_Design_Using_OpenLANE

## Table of Contents
**1. Day 1**
-  [How to talk to computers ](#how-to-talk-to-computers)
- [Introduction to RISCV ](#introduction-to-RISCV--)
-    [From Software Applications to Hardware](#from-software-applications-to-hardware--)
-    [SoC Design and OpenLANE](#soc-design-and-openlane)
-    [OpenLANE Installation](#openlane-installation-)

**2. Day 2**
- [Good and Bad Floorplanning , Placement and library cells](#day-2--good-and-bad-floorplanning--placement-and-library-cells)
- [Chip floorplanning consideration](#chip-floorplanning-consideration)
- [preplaced cells](#preplaced-cells)
- [decoupling capacitor](#decoupling-capacitor)
- [floorplan using openlane](#floorplan-using-openlane)
- [Initial Place Design](#initial-place-design)
- [Run placement in openlane](#run-placement-in-openlane)
- [Cell Design Flow](#cell-design-flow)
- [Characterization Flow](#characterization-flow)
- [Timing characterization](#timing-characterization)

**3. Day 3**
- [ Design Library Cell using magic and ngspice](#day-3--design-library-cell-using-magic-and-ngspice)
- [Inverter](#inverter)
- [CMOS Fabrication Process](#cmos-fabrication-process)
- [VSDST cell design lab](#vsdstdcelldesign-lab)
- [Magic DRC](#magic-drc)
- [Fix poly.9 error in sky.tech file](#fix-poly9-error-in-skytech-file)
- [Implement poly resistor spacing](#implement-poly-resistor-spacing)
- [Challenge exercise to describe DRC error](#challenge-exercise-to-describe-drc-error)
- [Lab challenge to find missing or incorrect rules (creating magic DRC rule)](#lab-challenge-to-find-missing-or-incorrect-rules-creating-magic-drc-rule)

**4. Day 4**  

 **Pre-Layout timing analysis and importance of good clock tree**  
 - [Convert grid info to track info](#convert-grid-info-to-track-info)
 - [Incorporating Custom Cells into OpenLANE Flow](#incorporating-custom-cells-into-openlane-flow)
 - [Introduction to Delay tables](#introduction-to-delay-tables)
 - [Custom Standard Cell Integration in the OpenLane Flow](#custom-standard-cell-integration-in-the-openlane-flow)
 - [Setup & Hold time](#setup--hold-time)
 - [Clock Jitter:](#clock-jitter)
 - [Clock Tree Synthesis](#clock-tree-synthesis)
 - [Crosstalk and clock net shielding](#crosstalk-and-clock-net-shielding)
 - [Lab Using TritonCTS](#lab-using-tritoncts)

**5. Day 5**  

**Final steps for RTL2GDS**	
- [Maze Routing and Lee's algorithm](#maze-routing-and-lees-algorithm)
- [Design Rule Check](#design-rule-check)
- [Power Distribution Network and routing](#power-distribution-network-and-routing)
- [Routing](#routing)
- [TritonRoute Features](#tritonroute-features)

- [References](#references)
- [Acknowledgement](#acknowledgement)
 
# Day_1 :Inception of open-source EDA, OpenLANE and Sky130 PDK  

## How to talk to computers 
## Introduction  :

A QFN-48 package is a type of integrated circuit (IC) package that contains a semiconductor chip (or die) at its core. The package has 48 pins or pads on its exterior, which are used for connecting the chip to other components on a circuit board. Inside the package, the core houses the chip (die) and may include additional features like thermal pads or ground connections, known as integrated passive components (IPs), to enhance the performance and thermal management of the IC.  

        
Inside the QFN-48 package, the semiconductor chip, or die, is situated at the core. This is the heart of the IC, where all the electronic functions and computations take place. In addition to the die, some QFN-48 packages may include integrated passive components (IPs). These can consist of elements like thermal pads for effective heat dissipation, which is crucial for maintaining the chip's optimal operating temperature, or ground connections to enhance electrical performance.  

A foundry, in the context of semiconductor manufacturing, refers to a specialized facility where semiconductor wafers are fabricated and integrated circuits (ICs) are produced. Foundries are crucial in the semiconductor industry because they serve as manufacturing partners for fabless semiconductor companies and even some integrated device manufacturers (IDMs) that do not own their own fabrication facilities.

Below is the representation :  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/04a355f9-f6fc-4d44-ba52-0adaa7f6ff04)

## Introduction to RISCV  :

RISC-V is an open-source instruction set architecture (ISA) designed for use in computer processors. It's named after the five "RISC" principles: Reduced Instruction Set Computing. Unlike proprietary ISAs like x86 (used by Intel and AMD) and ARM (used by various companies, including Apple and Qualcomm), RISC-V is open and freely available for anyone to use, modify, and implement. So C program will compile into assembly language and then converted into binary format. This binary will execute on the layout itself.  

RISC-V is a versatile and open ISA that has the potential to disrupt the semiconductor industry by democratizing processor design and enabling a wide range of applications. Its openness, simplicity, and flexibility make it an attractive choice for both industry professionals and educational institutions.
  Below shown the flow :
  
  ![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/eb9e5b13-cd78-456f-a42d-34be73a3bcba)

## From Software Applications to Hardware  :

In the realm of software applications, tasks are executed by the central processing unit (CPU) of a computer or device. Software programs provide instructions for the CPU to follow, and the CPU performs calculations, data processing, and various other operations based on these instructions. While software is flexible and can be updated easily, it may not always provide the highest level of performance or efficiency, especially for demanding or specialized tasks.  
  
          
The benefits of this transition from software to hardware include faster execution of tasks, lower power consumption, and the ability to handle specialized workloads with greater efficiency. However, it also means that the functionality is fixed and less adaptable compared to software, which can be updated or changed more easily.  
Below is shown the representation :  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/c70e58e7-5f68-477f-ac9c-8b117e34f8f3)

## SoC Design and OpenLANE

SoC (System-on-Chip) design using OpenLane refers to the process of creating complex integrated circuits that contain multiple components, including processors, memory, and various peripherals, using the OpenLane open-source digital ASIC (Application-Specific Integrated Circuit) design flow  

1. **System-on-Chip (SOC) Design** : SOC design involves integrating various components, such as CPUs, GPUs, memory, and interfaces, onto a single chip. This approach offers advantages in terms of size, power efficiency, and performance for a wide range of applications, from smartphones to IoT devices.
2. **OpenLane** : OpenLane is an open-source ASIC design flow developed by the Google-sponsored Skywater PDK (Process Design Kit) team. It provides a comprehensive set of tools and scripts that enable engineers and designers to automate the entire SOC design process, from RTL (Register-Transfer Level) design to GDSII (Graphic Data System II) tapeout.
3. **Skywater PDK**: OpenLane is compatible with the Skywater PDK, which provides the process-specific information and design rules needed for a specific semiconductor manufacturing process. The Skywater PDK is also open-source and maintained by Skywater Technology Foundry.
4. **Community Support**:  OpenLane has an active and growing community of users and contributors who share knowledge and collaborate on improving the toolchain. This collaborative effort helps enhance the capabilities and reliability of the platform.

Below is the OpenLANE Flow:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/b34a5d04-88e4-4d33-b890-70cf6ce55291)  

Below is the simplified flow:  

1. **RTL Design (Register-Transfer Level)**: At this stage, engineers create a high-level description of the desired chip's functionality using a hardware description language like VHDL or Verilog. This description defines how data moves between registers and logic gates in the chip.

2. **Synthesis**: The RTL code is synthesized into a gate-level representation. This step transforms the high-level description into a netlist of logic gates that can be implemented in silicon. Optimization techniques are applied to improve performance, power consumption, and area usage.

3. **Floorplanning**: Engineers create a layout plan, or floorplan, that specifies where different functional blocks will be placed on the chip. This step considers factors like power distribution and signal routing.

4. **Placement** : The synthesized gates are physically placed on the chip according to the floorplan. This step aims to minimize the physical distance between related gates to improve performance.

5. **Routing**: Wires are connected between the gates to establish the logical connections defined in the RTL code. This step involves complex algorithms to optimize for speed, power, and area.

6. **Physical Verification** : The design is thoroughly checked for issues like timing violations, manufacturing defects, and design rule violations. Tools ensure that the chip will function correctly and be manufacturable.

7. **Mask Generation**: The final layout, or mask, is generated based on the design. This mask provides a blueprint for the semiconductor fabrication process.

8. **Manufacturing**: The mask is used to manufacture the physical semiconductor wafer in a semiconductor fabrication facility (fab). This involves a series of intricate processes, including photolithography, etching, and doping, to create the actual chip.

9. **Testing**: After fabrication, each chip is rigorously tested to identify defects and ensure functionality.

10. **Packaging**: The individual chips are packaged into protective casings that include pins or connectors for interfacing with other electronic components.

11. **GDS2 Format**: GDS2 is a file format used to represent the final chip layout and mask data. It contains information about the physical layout of the chip, including the positions of gates, wires, and other elements.

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/4034abc0-e980-45f7-b491-2f6602d27768)

### OpenLANE and Strive Chipsets :  
OpenLane is an open-source Very Large Scale Integration (VLSI) flow that is designed to be highly configurable and easy to use for digital synthesis and backend flow. It is built around open-source tools and is a collection of scripts
that run these tools in the right order, transforming their inputs and outputs as appropriate, and organizing the results. OpenLane, along with the 130nm Process Design Kit (PDK), is part of a recent effort by various industry players 
to democratize Application-Specific Integrated Circuit (ASIC) design.  

On the other hand, Strive chipsets are a family of RISC-V System on Chips (SoCs) designed using the SkyWater 130nm process. RISC-V is an open standard instruction set architecture (ISA) based on established reduced instruction set 
computer (RISC) principles.  

Below shown StriVe SOC Family features:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/7e287129-fbbf-453c-9110-aa36ab073570)

Below is the OpenLANE ASIC flow :  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/9a9967c1-15f8-40b8-81fa-f02925bb8155)

**Antenna Rules Violations** : Antenna rules violations occur when certain parts of a semiconductor device, typically thin gate oxide regions (such as in MOS transistors), accumulate a significant charge during the manufacturing process. This charge can become trapped and cause unintended behavior in the circuit, such as latch-up (an undesirable state where the device draws excessive current) or other reliability problems.

**Cause** : Antenna rules violations are usually a result of the manufacturing process steps, like photolithography and etching, where charge accumulates on certain parts of the chip's surface due to the exposure to radiation or plasma. When the chip is later powered up, this trapped charge can cause issues.  

Below are the solutions:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/c3cc3f25-b129-4a93-925a-510773217976)

## OpenLANE Installation :

**Step 1- Installation of required packages**

```
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git
```

**Step 2-Docker Installation**

```
# Remove old installations
sudo apt-get remove docker docker-engine docker.io containerd runc
# Installation of requirements
sudo apt-get update
sudo apt-get install \
   ca-certificates \
   curl \
   gnupg \
   lsb-release
# Add the keyrings of docker
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
# Add the package repository
echo \
   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
# Update the package repository
sudo apt-get update

# Install Docker
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

# Check for installation
sudo docker run hello-world
```

**Step 3-Installing OpenLANE**

```
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```

Below shown the installation done : 

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/73a56577-19d8-42c4-9e70-6271a8d67c0b)

Now we will do run_synthesis :  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/e521c68b-fdc9-4950-918b-50a6b9b7a26d)

Below is dff_synthesis report:  

![synthrpt](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/c4d04351-021f-4c56-9327-c88d52a8cd8f)

![synthrpt2](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/ac2cc982-f792-4251-9b1b-b337f8bdba4b)


![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/686d8a71-a016-4b77-83b2-2b3625f4cf91)

Below is synthesis_pre report:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/f73e82ad-a3bd-4a95-aa71-8542b4f47ebd)


# DAY 2 : Good and Bad Floorplanning , Placement and library cells

## Chip floorplanning consideration
### Utilization factor and aspect ratio:  

### Core:
**The width** of the core typically refers to the physical size or dimensions of the central processing unit (CPU) or processor core within a microchip. It is usually measured in nanometers (nm) or micrometers (µm). For example, you might hear about a "14nm core" or a "7nm core," indicating the feature size of the core's transistors.  
**The height** of the core is not commonly referred to in the same way as the width. Instead, the core's size is usually described in terms of its area, which is determined by multiplying its width and height.  

### Die  (also known as the chip or silicon die):
 **The width** of the die is typically the physical measurement of the semiconductor wafer after all the individual ICs (integrated circuits) have been fabricated on it but before they are cut apart. Die widths can vary significantly depending on the specific manufacturing process and the design of the chips being produced. They can range from a few millimeters to several centimeters or more.  

 Similar to the core, **the height** of the die is not a common parameter of discussion. Instead, the die's size is often described in terms of its area, which is the product of its width and height.

Below is the representation : 

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/f8d3ab82-2bff-41f7-b9b7-a9d93cc291a9)

Below shown the utilization factor:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/f38d85a1-6629-455e-9a8f-7d66b8e900c5)

### Preplaced Cells:
Pre-placed cells, often referred to as "pre-placed blocks" or "pre-placed logic cells," are a concept used in digital integrated circuit design. They are a specific type of logic cell or block that is manually placed by a designer in a fixed position on the semiconductor die or chip during the design process. These cells serve various purposes and provide several advantages in the chip design process.    

Unlike standard cells in a digital design, which are typically placed automatically by place-and-route tools, pre-placed cells are manually positioned by the designer. The designer selects specific locations on the chip for these cells based on design considerations, performance requirements, or other constraints.  

Pre-placed cells are often used for critical components of a design, such as memory blocks, analog modules, or specialized digital circuits that need to be precisely located to meet performance, power, or area constraints. Placing them manually ensures that they are in the optimal positions for meeting these requirements.  

In large and complex chip designs, pre-placed cells can be used to create a hierarchical structure, where certain functional blocks or subsystems are pre-placed and interconnected. This approach simplifies the overall design process and allows for better management of the design's complexity.   

Below is the more detailed representation:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/1721de55-1098-4791-a570-81727ed0f400)

### Decoupling capacitor:  
 Decoupling capacitors are essential components in electronic circuit design that help maintain a stable power supply, filter out noise, and improve the overall performance and reliability of electronic systems, particularly in digital and mixed-signal applications. Proper selection, placement, and sizing of decoupling capacitors are critical for their effectiveness in reducing noise and maintaining voltage stability.  

 ![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/b9bb119f-d746-4505-b0dc-5c4bcf7208ea)


**Noise margin** is a concept used in digital electronics and integrated circuit (IC) design to quantify the tolerance of a digital signal to noise and voltage variations. It provides a measure of the robustness of a digital circuit by defining the range of acceptable voltage levels for logic values (0 and 1) and ensuring that signals can be reliably interpreted in the presence of noise. Noise margin is typically expressed in terms of voltage or voltage range.

Below is representation:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/a85440af-c92b-4df9-beaf-0971f0308ca9)

**Power Planning** in integrated circuit (IC) design is a crucial aspect of ensuring proper power distribution to various components on the chip. While pre-placed macros (blocks) may have dedicated decoupling capacitors (decaps) for noise filtering and stabilization, the entire chip can't have individual decaps. To address this, effective power planning involves creating a network of VDD (power supply) and VSS (ground) pads for each block, strategically connecting them to horizontal and vertical power and ground lines. These lines form a power mesh, which acts as a distributed power delivery network. This approach ensures that each block receives a stable and clean power supply, reducing noise and voltage fluctuations, and contributes to the overall reliability and performance of the integrated circuit. The power mesh effectively distributes power throughout the chip, preventing voltage drops and ensuring consistent operation of all blocks.  


**Pin Placement** in integrated circuit (IC) design involves determining the physical locations of input and output (I/O) pins that connect to the logic gates within the chip.  
The netlist specifies how the logic gates within the chip are interconnected. It provides information about which gates are connected to one another and how signals flow through the design.  
After the I/O pad positions are determined, the design process includes logical placement blocking of pre-placed macros. This step involves arranging pre-placed macros (blocks of predefined logic) in a way that distinguishes them from the area reserved for the I/O pins. This separation ensures that the macros do not interfere with the connectivity and signal paths associated with the pins.  

### FLoorplan using OpenLANE
To run the picorv32a floorplan in openLANE:
```
run_floorplan
```

To view the floorplan, Magic is invoked after moving to the results/floorplan directory:
```
magic  /home/pruthvi/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.min.lef def read picorv32a.def 
```

Below is the representation:  

![Screenshot 2023-09-07 201916](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/1b601780-1297-470e-9886-b57f32326c22)

![Screenshot 2023-09-07 202014](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/5342f33b-d5a0-4333-8cf3-9f54289bbda0)

## Initial Place Design

Here below shown **Optimize Placement Using Estimated Wire Length And Capacitance** representation : 

![optimizeplace](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/25f8acdf-7917-4646-8757-01d681b9bf2b)

Here above we have to connect Din1 to Dout1 so there are FFs and wire shown .  
Optimizing placement in integrated circuit design involves arranging the components on a chip to achieve specific goals. Two important factors in this optimization are wire length (the length of connections between components) and capacitance (which affects power and timing).

**Library characterization** is the process of characterizing electronic components and gates, such as logic gates, flip-flops, and other building blocks, to create models that accurately represent their behavior under various conditions. This characterization provides information about how components respond to different inputs, delays, power consumption, and more.  

**Library modeling** involves creating mathematical or algorithmic representations of the behavior and characteristics of components. These models are used by EDA tools to simulate, analyze, and optimize digital circuits during the design phase. 

Here below is the representation of the flow:  

![optflow](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/9a01cb34-6a44-4519-b355-a3c707d84b9b)

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/e63f4f18-c5e3-4d5e-97ad-d543ec7f3936)


**Logic synthesis** is a crucial step in the design of digital integrated circuits (ICs) and plays a central role in transforming a high-level hardware description into a gate-level representation that can be fabricated in silicon.  

**Floorplan** is one the critical & important step in Physical design. Quality of your Chip / Design implementation depends on how good is the Floorplan. A good floorplan can be make implementation process (place, cts, route & timing closure) cake walk. On similar lines a bad floorplan can create all kind issues in the design (congestion, timing, noise, IR, routing issues). A bad floorplan will blow up the area, power & affects reliability, life of the IC and also it can increase overall IC cost (more effort to closure, more LVTS/ULVTS).

**Placement** is the process of determining the locations of circuit devices on a die surface. It is an important stage in the VLSI design flow, because it affects routabil- ity, performance, heat distribution, and to a less extent, power consumption of a design.

**Clock Tree Synthesis** is a technique for distributing the clock equally among all sequential parts of a VLSI design. The purpose of Clock Tree Synthesis is to reduce skew and delay.

**Routing** in VLSI is making physical connections between signal pins using metal layers. Following Clock Tree Synthesis (CTS) and optimization, the routing step determines the exact pathways for interconnecting standard cells, macros, and I/O pins.

### Run placement in OpenLANE

Below is the command to run placement in openlane 

```
run_placement
```
Below will be the result :  

![placement](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/9b662b77-80bf-413c-a253-c59a99cfeee2)

![place](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/76ff3d99-f329-4d6a-b1ea-350f5dbfd85b)

## Cell Design Flow 

Below is the representation of cell design flow

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/d9b0c205-02eb-4517-932b-9342274a604e)

**Cell design flow**, also known as standard cell design flow, is the process of creating and optimizing standard cell libraries used in digital integrated circuit design. These libraries contain fundamental building blocks, such as logic gates and flip-flops, that are used to design complex digital circuits.

1. **Specification and Requirements**:
Begin by defining the specifications and requirements for the standard cell library. This includes factors like technology node, voltage levels, speed requirements, and power constraints.

2.**Cell Architecture Selection**: Choose the architecture and topology for the standard cells. This involves deciding on the logical functions each cell will implement and the number of input and output pins.

3. **Schematic Design**: Create schematic designs for each standard cell. This involves designing the logical function of the cell using gates and interconnections. Tools like schematic capture software are used for this step.

4. **Simulation and Verification**:
Simulate the designed cells to verify that they meet the specified functionality and timing requirements. This step may include functional simulation, static timing analysis (STA), and power analysis.

5. **Layout Design**:
Create physical layouts for the cells based on the schematic designs. This involves specifying the dimensions, placement of transistors, and routing of metal layers.

6.**DRC and LVS Check**s:
Perform Design Rule Check (DRC) and Layout vs. Schematic (LVS) checks to ensure that the layout adheres to the manufacturing rules and is consistent with the schematic.

7.**Extraction and Characterization**:
Extract parasitic components from the layout, including resistances and capacitances. These parasitics impact the timing and power characteristics of the cells.
Characterize the cells by measuring their performance under various conditions, such as different input vectors and operating voltages.

8.**Timing Analysis**: Conduct detailed timing analysis to determine parameters like propagation delay, setup time, hold time, and clock-to-q delay for flip-flops.  

9.**Library Validation**:
Validate the entire standard cell library by using it in test chip or design test cases to ensure that it meets performance and functionality requirements.

Below is the flow:  

![cellflow](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/7367738e-b8a8-45c1-a807-510dc8decc58)

Below shown the different functionality of different size of library that consists of gates dffs and latches.

![flow2](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/3bf02762-0122-4b5d-9c58-745e05c5c90a)

![flow3](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/ee3e78d5-09f3-44e0-95ac-85b0fe46420e)

Below is the stick art layout diagram representation: 

![stick](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/c8686751-6c19-45fe-b1bc-e27a9b0ed337)


### Characterization Flow

**Characterization** in VLSI refers to the process of analyzing and documenting the electrical behavior of electronic components, such as transistors, logic gates, memory cells, and standard cells, under various operating conditions. Characterization is essential for accurate circuit simulation and helps ensure that integrated circuits (ICs) meet their performance, power, and timing requirements.

  
Let's see below flow representation:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/373629ea-83eb-4407-8147-065241d522de)

![charactflow](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/b85d4dbf-c696-4945-8142-e463ed06439e)

![till7](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/c437f4e7-8f99-470e-a963-55fa785759ea)

![8thstep](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/47270b71-857c-4c2a-9352-f07d8f9f1187)


### Timing characterization 

**Timing characterization** is essential for ensuring that digital circuits meet their timing requirements. It involves determining the timing behavior of various elements within the IC, such as logic gates, flip-flops, and interconnections, under different operating conditions.

**Setup Time**: The amount of time before the clock edge that data must be stable to be correctly captured by a flip-flop.
**Hold Time**: The amount of time after the clock edge that data must remain stable to be correctly captured.

**Delay Calculation**:  
Characterize the delays of logic gates, flip-flops, and interconnects.
Calculate the propagation delay from the input of a circuit element to its output.  

**Clock Skew Analysis**:
Analyze the variation in clock arrival times at different parts of the circuit.
Clock skew can impact the synchronization of sequential elements and can be critical in high-speed designs.  

 **Corner Case Characterization**:
- Perform timing characterization under different process corners (fast corner and slow corner) to account for manufacturing variations.
- Analyze worst-case scenarios to ensure robust operation.

**Post-Layout Timing Analysis**:
- After physical design and layout, perform post-layout timing analysis to account for the actual interconnection delays and verify that the design still meets timing constraints.

Below shown delay analysis : 

```
time(out*thr) - time(in*thr)
```

![delay1](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/d70c1d5c-1237-4de7-a7be-33a43244ba61)

Below is the graphical representation:  

![delay2](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/1b445c87-f5eb-49b1-9944-e64de07d1086)

Below is the slew low and high threshold : 

![delay3](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/4c27bb89-67f7-416f-ab1d-ac7afc01bc3f)

![delay4](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/f1ed1a35-5410-42b9-b36a-83904fe4c89c)

Below is the timing threshold definitions:  

![timing2](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/dd35c690-12e5-4a01-872e-153ca1d1b581)

![timingdef](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/626faea1-9572-42b7-8b8b-bfa9aef71048)

# DAY 3 : Design Library Cell using magic and ngspice

### Inverter

A **CMOS inverter**, short for Complementary Metal-Oxide-Semiconductor inverter, is a fundamental digital electronic circuit that performs the basic logical operation of inversion. In other words, it takes an input signal and produces an output signal that is the logical complement of the input. If the input is high (logic 1), the output will be low (logic 0), and vice versa.  

The input signal is applied to the gate terminals of both the NMOS and PMOS transistors. The output is taken from the connection point (the drain of NMOS and the source of PMOS) between these two transistors.  

**NMOS Operation**: When the input is logic high (1), the NMOS transistor turns on because a positive voltage is applied to its gate. This establishes a low-resistance path between the output and ground, causing the output to be pulled to logic low (0).  

**PMOS Operation**: Conversely, when the input is logic low (0), the PMOS transistor turns on because a low voltage is applied to its gate. This establishes a low-resistance path between the output and the power supply voltage (VDD), causing the output to be pulled to logic high (1).


Below shown the inverter diagram : 

![inverter](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/c0f143c3-3806-4d74-a701-2d38e8475298)

Below shows nodes:   

![2inverternodes](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/08d0db99-e46f-447c-80b5-7227ad9fadbc)

Here is spice deck simulation shown:  

![3spicedeck](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/db0c1c30-0a35-417d-80b8-d48ec66ec503)

Here is a cmos.cir file: 

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/013b3083-47b6-42c4-a65b-d52916dee748)

Below is the model file : 

```
* SPICE 3f5 Level 8, Star-HSPICE Level 49, UTMOST Level 8

.lib cmos_models 
* DATE: Feb 23/01
* LOT: T0BM                  WAF: 07
* Temperature_parameters=Default
.MODEL nmos  NMOS (                                LEVEL   = 49
+VERSION = 3.1            TNOM    = 27             TOX     = 5.8E-9
+XJ      = 1E-7           NCH     = 2.3549E17      VTH0    = 0.3907535
+K1      = 0.4376003      K2      = 8.265151E-3    K3      = 4.214601E-3
+K3B     = -3.7220937     W0      = 2.517345E-6    NLX     = 2.310668E-7
+DVT0W   = 0              DVT1W   = 0              DVT2W   = 0
+DVT0    = 0.2411602      DVT1    = 0.3707226      DVT2    = -0.5
+U0      = 316.5922683    UA      = -9.89493E-10   UB      = 2.154013E-18
+UC      = 2.474632E-11   VSAT    = 1.254499E5     A0      = 1.2735648
+AGS     = 0.2428704      B0      = 2.579719E-8    B1      = -1E-7
+KETA    = 4.87168E-4     A1      = 0              A2      = 0.5196633
+RDSW    = 120            PRWG    = 0.5            PRWB    = -0.2
+WR      = 1              WINT    = 2.357855E-8    LINT    = 1.210018E-9
+DWG     = 2.292632E-9
+DWB     = -9.94921E-10   VOFF    = -0.1039771     NFACTOR = 1.3905578
+CIT     = 0              CDSC    = 2.4E-4         CDSCD   = 0
+CDSCB   = 0              ETA0    = 3.894977E-3    ETAB    = 7.800632E-4
+DSUB    = 0.0307944      PCLM    = 1.7312397      PDIBLC1 = 0.999135
+PDIBLC2 = 4.850036E-3    PDIBLCB = -0.0866866     DROUT   = 0.8612131
+PSCBE1  = 7.995844E10    PSCBE2  = 1.457011E-8    PVAG    = 0.0099984
+DELTA   = 0.01           RSH     = 5              MOBMOD  = 1
+PRT     = 0              UTE     = -1.5           KT1     = -0.11
+KT1L    = 0              KT2     = 0.022          UA1     = 4.31E-9
+UB1     = -7.61E-18      UC1     = -5.6E-11       AT      = 3.3E4
+WL      = 0              WLN     = 1              WW      = -1.22182E-16
+WWN     = 1.2127         WWL     = 0              LL      = 0
+LLN     = 1              LW      = 0              LWN     = 1
+LWL     = 0              CAPMOD  = 2              XPART   = 0.4
+CGDO    = 3.11E-10       CGSO    = 3.11E-10       CGBO    = 1E-12
+CJ      = 1.741905E-3    PB      = 0.9876681      MJ      = 0.4679558
+CJSW    = 3.653429E-10   PBSW    = 0.99           MJSW    = 0.2943558
+CF      = 0              PVTH0   = -0.01          PRDSW   = 0
+PK2     = 2.589681E-3    WKETA   = -1.866069E-3   LKETA   = -0.0166961      )
*
.MODEL pmos  PMOS (                                LEVEL   = 49
+VERSION = 3.1            TNOM    = 27             TOX     = 5.8E-9
+XJ      = 1E-7           NCH     = 4.1589E17      VTH0    = -0.583228
+K1      = 0.5999865      K2      = 6.150203E-3    K3      = 0
+K3B     = 3.6314079      W0      = 1E-6           NLX     = 1E-9
+DVT0W   = 0              DVT1W   = 0              DVT2W   = 0
+DVT0    = 2.8749516      DVT1    = 0.7488605      DVT2    = -0.0917408
+U0      = 136.076212     UA      = 2.023988E-9    UB      = 1E-21
+UC      = -9.26638E-11   VSAT    = 2E5            A0      = 0.951197
+AGS     = 0.20963        B0      = 1.345599E-6    B1      = 5E-6
+KETA    = 0.0114727      A1      = 3.851541E-4    A2      = 0.614676
+RDSW    = 1.496983E3     PRWG    = -0.0440632     PRWB    = -0.2945454
+WR      = 1              WINT    = 7.879211E-9    LINT    = 2.894523E-8
+DWG     = -1.112097E-8
+DWB     = 9.815716E-9    VOFF    = -0.1204623     NFACTOR = 1.2259401
+CIT     = 0              CDSC    = 2.4E-4         CDSCD   = 0
+CDSCB   = 0              ETA0    = 0.3325261      ETAB    = -0.0623452
+DSUB    = 0.9206875      PCLM    = 0.833903       PDIBLC1 = 9.948506E-4
+PDIBLC2 = 0.0191187      PDIBLCB = -1E-3          DROUT   = 0.9938581
+PSCBE1  = 2.887413E10    PSCBE2  = 8.325891E-9    PVAG    = 0.8478443
+DELTA   = 0.01           RSH     = 3.6            MOBMOD  = 1
+PRT     = 0              UTE     = -1.5           KT1     = -0.11
+KT1L    = 0              KT2     = 0.022          UA1     = 4.31E-9
+UB1     = -7.61E-18      UC1     = -5.6E-11       AT      = 3.3E4
+WL      = 0              WLN     = 1              WW      = 0
+WWN     = 1              WWL     = 0              LL      = 0
+LLN     = 1              LW      = 0              LWN     = 1
+LWL     = 0              CAPMOD  = 2              XPART   = 0.4
+CGDO    = 2.68E-10       CGSO    = 2.68E-10       CGBO    = 1E-12
+CJ      = 1.864957E-3    PB      = 0.976468       MJ      = 0.4614408
+CJSW    = 3.118281E-10   PBSW    = 0.6870843      MJSW    = 0.3021929
+CF      = 0              PVTH0   = 6.397941E-3    PRDSW   = 30.410214
+PK2     = 2.100359E-3    WKETA   = 5.428923E-3    LKETA   = -0.0111599      )
*
.endl
```

![1ngspice](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/7beb4d5c-48ab-428d-a04a-0dfa258192b2)


to run it open ngspice and in command give :  

```
source cmos.cir
```

![2ngspice](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/328c0c48-2b89-46b3-8073-b10ff8f2b56d)


To execute it : 

`
run
`
Then using `setplot` you can set the dc plot.  
Also you can see by usign `display`  

Now using `plot out vs in` Below graph will be seen:  

![plot](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/a7d70792-0e1b-4832-97ec-3ac5af4fd2b6)

Now if we increase the width of pmos which is `0.9375` below graph is seen and you can compare it with the above graph :  

![shiftplot](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/8772dcb3-772b-4da2-bebe-c1cb717cbb7d)

Below shown switching threshold representation where `Wp/Lp and xWn/Ln` relation and calculation shown: 

![4switchthreshold](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/be436190-b7b5-49d1-8cb7-98dd18e6324d)


Below is the modified cmos file:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/271af951-0287-4ea5-83b3-1b700bace805)

Here is the graph of `out vs time` 

![ckt2OutvsTime](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/d17a1a4e-8c0d-49a1-a6dd-9d5ec2876083)

Now here is the graph of `out vs time in`

![ckt2OutvsTimeIn](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/b63e5e15-85bc-4570-8ab7-0931995cf250)

To find the difference between two graph points just drag with mouse and it will zoom and then you can just click on the graph.  
It will show the points in ngspice terminal:  

![2diffckt2OutvsTimeIn](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/176fb2ef-fb76-4d81-9687-84075023721e)

![diffckt2OutvsTimeIn](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/85cf86c9-defc-494e-a6a8-80c77c60aa77)


### CMOS Fabrication Process  


The 16-mask CMOS fabrication process is explained below :  


1. **Substrate Selection**: Selecting a substrate is a important step in semiconductor manufacturing and integrated circuit (IC) fabrication. The substrate is the foundational material upon which the entire IC will be built. Typically, silicon (Si) is the most commonly used substrate material for most modern ICs due to its favorable properties, but other materials like gallium arsenide (GaAs) or silicon carbide (SiC) are also used in specific applications.
2. **Creating active region for transistors**: Creating active regions for transistors involves isolating specific areas on a silicon substrate where transistors will be located. This isolation is achieved by depositing layers of silicon dioxide (SiO2) and silicon nitride (Si3N4) on the substrate. Then, using photolithography and etching techniques, patterns are defined on the silicon nitride layer. These patterns determine where the active regions for transistors will be. The remaining SiO2 and exposed silicon regions become the isolated pockets where transistor components will be fabricated. This isolation is crucial to prevent unwanted electrical interactions between transistors and ensure their proper functioning.
3. **N-well and P-well formation**: The formation of N-well and P-well regions in CMOS technology involves ion implantation using specific dopants. Boron is utilized for P-well formation, while Phosphorus is employed for N-well creation. These dopants are implanted into the silicon substrate to define the N-well and P-well regions, which are essential components for building complementary NMOS and PMOS transistors, respectively.

4. **Formation of gate terminal**: The gate terminals for NMOS (N-channel Metal-Oxide-Semiconductor) and PMOS (P-channel Metal-Oxide-Semiconductor) transistors are created through photolithography techniques. In this process, precise patterns are defined on the semiconductor substrate using masks and light exposure. These patterns correspond to the gate electrodes of the transistors, and they play a fundamental role in controlling the transistor's conductivity and operation. By carefully implementing photolithography, the gate terminals for both NMOS and PMOS transistors are formed with high precision, enabling the subsequent steps in transistor fabrication.  
5. **LDD (lightly doped drain) formation:** In the LDD process, additional ion implantation steps are introduced after the formation of the main source and drain regions of the transistor. The key idea is to create lightly doped regions adjacent to the main source and drain regions. These lightly doped regions serve as a buffer between the channel and the heavily doped source and drain regions. The purpose of the LDD regions is to reduce the strength of the electric field near the drain, particularly in the region where the channel meets the drain. This helps to prevent the acceleration of electrons to high energies, which can lead to the hot electron effect. The hot electron effect can cause damage to the gate oxide and result in long-term reliability issues for the transistor.
6. **Source & drain formation:** The formation of the source and drain regions in a semiconductor device is a critical step in the fabrication process. To ensure proper performance and avoid issues like channeling during ion implantation, several techniques are employed, including the use of a screen oxide layer, arsenic implantation, and annealing.  **Screen Oxide**: Before performing the source and drain ion implantation, a thin layer of screen oxide is deposited or grown on the semiconductor wafer's surface. The screen oxide serves as a protective layer during the implantation process. It helps to disperse and slow down the implanted ions, reducing the likelihood of channeling.  **Arsenic Implantation**: Arsenic (As) ions are implanted into the regions of the silicon substrate where the source and drain are to be formed. Arsenic is a common dopant used for N-type (electron-conducting) regions in CMOS technology. The implantation process introduces a controlled amount of arsenic atoms into the silicon lattice, creating N-type doping in the source and drain regions.  **Annealing**: After the arsenic implantation, the wafer is subjected to an annealing process. Annealing involves heating the wafer to high temperatures for a specified duration. During annealing, the implanted arsenic ions are activated, and any damage to the silicon crystal lattice caused by the implantation process is repaired. Annealing helps to ensure that the source and drain regions have the desired electrical properties.
7. **Local interconnect formation:** Local interconnect formation is a important step in semiconductor device fabrication, enabling the creation of electrical connections between different components on a chip.  **Screen Oxide Removal (HF Etching):** After various processing steps, including source and drain formation, a screen oxide layer is typically deposited or grown on the semiconductor wafer's surface. This screen oxide layer serves as a protective barrier during ion implantation. However, it needs to be removed to allow for the formation of local interconnects.
**HF Etching:** Hydrofluoric acid (HF) is commonly used to selectively etch away the screen oxide. HF is highly effective at removing silicon dioxide (SiO2) while leaving other materials like silicon (Si) and metal layers unaffected.  **Deposition of Ti (Titanium):** Once the screen oxide is removed, the next step involves depositing a layer of titanium (Ti) onto the wafer's surface. Titanium is chosen for its excellent adhesion properties and low electrical resistance.
**Low-Resistance Contacts:** Titanium serves as the base layer for creating low-resistance electrical contacts or interconnects. It acts as an adhesion layer for subsequent metal layers (typically aluminum or copper) that will be deposited to form the actual interconnects.
8.**Higher level metal formation:** The higher-level metal formation in semiconductor device fabrication involves creating additional layers of metal interconnects to connect various components and ensure proper functionality.  **Chemical-Mechanical Polishing** (CMP) for Planarization: After the initial layers of metal interconnects and insulating layers have been deposited and patterned, the surface of the wafer can become uneven due to the topography of the underlying structures. To ensure a flat and planar surface, CMP is employed.
**CMP**: Chemical-Mechanical Polishing is a process that uses a combination of chemical etching and mechanical abrasion to remove excess material and achieve a smooth, flat surface. It is important for ensuring uniform layer thickness in subsequent metal layers.  **Top SiN (Silicon Nitride) Layer for Chip Protection:** To protect the completed chip from environmental factors, moisture, and physical damage, a top layer of silicon nitride (SiN) is deposited. Silicon nitride is an excellent insulator and provides a robust protective barrier.
**Chip Protection:** This top SiN layer acts as a passivation layer, shielding the underlying components from external influences. It also helps prevent contamination and ensures the long-term reliability of the integrated circuit.

Below is the final representation:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/719e565b-fa42-4d56-b82f-8550730bd940)



### VSDSTDCelldesign Lab 

First git clone the vsdstdcelldesign repository using below command :  

``
git clone https://github.com/nickson-jose/vsdstdcelldesign
``  

There will be `sky130_inv.mag` file 

Use the sky130A.tech file from the `libs` folder when you are running the magic.

To run the layout design in magic use the below command :  

```
magic -T sky130A.tech sky130_inv.mag &
```

![1](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/faddcf47-e351-49f6-a9f4-2f3536f30cde)

Now if you click on any component and type `what` in terminal it will tell about the component:  

![2whatnmos](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/16f547de-44bd-45dc-9e11-b2fb1f0e7f9a)

Here shown the output terminal :  

![3whaty](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/a897de8c-e624-4887-ba49-70a71affac5f)

Now to understand this stick diagram below is representation where pdiff, ndiff, poly etc are shown:  

![4cmosinfo](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/571d6378-d4b8-4fd4-b393-fc039331f4ed)

**Pdiff (p-diffusion)**: Pdiff represents the P-diffusion layer in a CMOS process. This layer is used to create the N-channel MOSFETs (NMOS) in the CMOS technology. It typically represents regions where the silicon substrate is doped with a P-type dopant, creating the source and drain regions of NMOS transistors.  

**Ndiff (n-diffusion**): Ndiff represents the N-diffusion layer in a CMOS process. This layer is used to create the P-channel MOSFETs (PMOS) in the CMOS technology. It typically represents regions where the silicon substrate is doped with an N-type dopant, creating the source and drain regions of PMOS transistors.  

**Poly (polysilicon)**: The Poly layer represents the polysilicon layer, which is used to form the gates of both NMOS and PMOS transistors. The gates control the flow of current between the source and drain regions in these transistors.  

**Pdcontact (p-diffusion contact)**: Pdcontact represents the contact points or vias used to make electrical connections to the P-diffusion layer. These contacts are used to connect metal layers to the P-diffusion regions.  

**Ndcontact (n-diffusion contact**): Ndcontact represents the contact points or vias used to make electrical connections to the N-diffusion layer. These contacts are used to connect metal layers to the N-diffusion regions.

**extthresh**: Using this command it is used to extract parasitic capacitance  

Now to extract it to spice use below command in magic terminal :  

``
ext2spice
``

It will create `sky130_inv.spice` file : 

![5spicefile](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/ab97542a-7543-49e5-80ea-b624ccb6ad46)

Now include the `pshort.lib` and `nshort.lib` libraries and modified the models. 

Then pulse is given in which format is below:  

`PULSE(V1 V2 Tdelay Trise Tfall Ton Tperiod Ncycles)`  

 Below is the modified spice file:  

 ![6modifiedinv](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/7a3685dc-e894-4a35-b42c-8a6bc829298e)

Now run it in ngspice :  

![7ngspiceshow](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/4d16af1e-a825-4b66-b517-a73286f63e36)

Now give below command :  

```
plot y vs time a
```

It will give below graph :  

![8ngplot](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/78931dd9-56d1-448f-93c3-8f79e0d40cd9)


Now if zoom the graph to find rise time difference here is the representation:  

![9-zoomgraph](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/5b29d1b2-1021-4b40-bc00-aed62ba86e00)

And then click on the graph it will show :  

![10value](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/dc2c5cb1-8e72-4d6d-a9fd-009e75637b2f)

## MAGIC DRC

You can read Magic user guide from : `http://opencircuitdesign.com/magic/` 

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/56354c85-f2f1-4dd8-a305-567ad241c664)

To use the lab contents below is the command:  

```
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
```

To extract the .tgz use below command:  

```
tar xfz drc_tests.tgz
```

Now in that extracted folder there are files like this :  

![drctest](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/a1f1c8b8-82ef-4a51-ae2d-5930579cd82c)

Now open the terminal to open the file give below commands:  

```
magic -d XR met3.mag
```
Below is the periphery rules for m3: (which can be found on `https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html#m3`)   

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/7d65c0c6-8bef-450e-8420-810376d593e4)


Below is the representation:  

![2meg3](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/045954d6-a9e0-4f74-b9ba-6c2c578d37fc)

Then with the mouse select the box and type the command it will show error of overlap, width spacing etc:  

``
drc why
``

![3errordrcwhy](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/79d04b91-b800-4379-9a1e-49d8f0041671)

Now create a box and hover over the metal3 on the sidepar and press 'p' on the keyboard (p for paint) , You can also undo by pressing the 'u' key :  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/eabab38d-bc25-43cd-b952-42b4e04be58e)

You can also make a box on elements to see metalcuts.  

Then type below command (to see metalcuts) in magic terminal :  

``
cif see VIA2
``

![4cifsee](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/f58eb19b-73b5-4aae-b1cc-0e191f58326f)

### Fix poly.9 error in sky.tech file

To load the poly.mag :  

``
load poly.mag
``

It will open layout of the file in magic:  

![5polymag](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/1252e6bb-00c5-4e46-9893-4b63f7c457fe)

You can see what are the elements by selecting it and type `what` in the terminal.  

Now edit the sky.tech file. Open it in the text editor using below command:  

`gedit sky130A.tech`

Now search for the `poly.9`there will be 2-3 results here is one of them :  

```
spacing npres *nsd 480 touching_illegal \
	"poly.resistor spacing to N-tap < %d (poly.9)"
```

Modify it to this :  

```
spacing npres allpolynonres 480 touching_illegal \
	"poly.resistor spacing to N-tap < %d (poly.9)"
```

Now it should be like this :  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/29b5038f-2a70-432b-b15a-5dfff7f2daf5)

Now update the other one :  

```
spacing xhrpoly,uhrpoly,xpc alldiff 480 touching_illegal \

	"xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"
```

Modify it to this:  

```
spacing xhrpoly,uhrpoly,xpc allpolynonres 480 touching_illegal \

	"xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"
```
It should be look like this:   

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/eed19458-b52a-4cac-8a58-cf9a0d2a92b6)

Now save it. You dont have to close the magic after the modifying the sky.tech file. Type the below command in magic's terminal:  

``
tech load sky130A.tech
``
In the warning click on yes.  
Then type below command:  

``
drc check
``

Below is the modified layout:  

![8copy](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/04d36d05-1814-4411-a29a-42454e82c433)

### Implement poly resistor spacing

Copy the three resistors by selecting (Edit > select area) and then press 'c' on keyboard.  
You can move the copied resistors by pressing 'm' key and arrow key.  

Now create n diffusion and p diffusion by creating box and selecting the `ndiff` and `pdiff` from the sidebar(by clicking the middle button of the mouse).  

Then modify the sky130A.tech file by just modifying the `*nsd` to `alldiff`.  
Now type below command in magic's terminal and all the rules will correctly identify :  

``
drc check
``

Below is the representation:  

![9npdiffusion](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/ca855626-edb1-464a-a4d8-e7ab3d302ac1)

### Challenge exercise to describe DRC error

Open sky130A.tech file and search `cifmaxwidth` below is the representation:  

![1](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/50f56848-6d90-4215-98f2-bfad07fc6f03)

Below is the rule shown for nwell (which can be access by skywater sky130 pdk website) :  

![3nwellrule](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/7d980717-2225-4bc5-8dcb-b2e3a7f0791b)

Also refer this dnwell rules:  

![2rule](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/407196cf-9a32-47fa-a29c-f0bc53812fb7)

Refer this style drc in sky130A.tech file :  

![4styledrc](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/daf3b70f-b1d3-44ab-9909-98a82ca63695)

First create a box around cell nwell6 , Now in tkcon terminal type below commands:  

![5nwell](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/b50367af-1061-496b-8e54-7687b3d035c7)

![6errornwell](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/6d8f0d4a-b97a-48c5-ae4b-3a39db94e552)


```
cif ostyle drc
cif see dnwell_shrink
feed clear
cif see nwell_missing
feed clear
```

Here shown the representations:  

![7shrink](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/b0292e43-8551-4a7b-8c70-36153cd1e5b9)


![8feedclear](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/1762a25e-92f7-44b3-80c5-2d1f70060d74)

![9final](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/4e0e24a9-a56a-49d3-92e5-6b7bfc6bd7b9)

### Lab challenge to find missing or incorrect rules (creating magic DRC rule)

Modify the sky130A.tech file according to below:  

change the cifmaxwidth code to this :  

```
cifmaxwidth nwell_untapped 0 bend_illegal \

	"Nwell missing tap (nwell.4)"
```

![ciffmax](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/cf237e7b-9017-4800-bc69-6de5204b55d9)

Then modify the nwell according to this :  

![nwellmodified](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/7a9dece1-35a2-4dcf-87eb-08d83daa8b39)

Below is the variant modification:  

![variants](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/05c855b0-7942-460b-b956-e8ae9f7f2a15)

After modification give commands shown below in terminal :  

``
tech load sky130A.tech
drc check
drc style drc(full)
drc check
``
See below there is no error for now :  

![4noerror](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/99f53718-f357-4351-9cea-6fdf37aec5b1)

![5drccheck](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/8b637453-83f2-42b5-a010-6282dbdb19d4)

Now tapp using nsubstratencontact shown below it will change DRC:  

![6final](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/760490cf-3bb4-4af9-b58f-3ea1288a77af)

# Day-4 : Pre-Layout timing analysis and importance of good clock tree

### Convert grid info to track info
Below is the track.info shown:  

![1trackinfo](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/59744ac3-c799-4ba3-bc6c-71d95c62b5b4)

Below is the before grid on representation:  

![2beforecon](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/51abb496-0289-4d3e-b0fb-ce6d6e86e2f4)

A key criterion outlined in the tracks.info specification is that ports must be positioned at the juncture of both horizontal and vertical tracks. Specifically, when dealing with the CMOS Inverter, ports A and Y are designated to reside within the li1 layer. It is imperative to guarantee that these ports are indeed situated precisely at the intersection of horizontal and vertical tracks.Below is the command:  

```
grid 0.46um 0.34um 0.23um 0.17um
```

Below is the after grid representation:  

![3aftergrid](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/cabab034-6360-4261-b5fe-5822570cbd97)

The subsequent step in the process involves the extraction of the LEF file for the completed layout of the cell. This crucial step is essential to facilitate the placement and routing tools effectively. It necessitates the precise specification of characteristics and definitions for the cell's pins. Ports, which represent the declared PINs of the macro, are encapsulated within a cell and are formatted as a macro cell in LEF files. Our primary objective is to generate an LEF file in a predefined format based on a given configuration, such as a straightforward CMOS inverter. To accomplish this, the initial task is to meticulously define each port and allocate the appropriate class and use attributes to each one.  

To establish the port configuration, you can utilize the Magic console, and here's a detailed breakdown of the steps involved:

Begin by opening the Magic Layout window.

Source the .mag file associated with your design, in this case, the inverter layout.

Navigate to the "Edit" menu and select "Text." This action will prompt a dialogue box to appear.

Within the dialogue box, double-click on the letter 'S' located at the I/O labels on the layout.

You will notice that the text field automatically populates with the appropriate string name and size for the port.

To finalize the port definition, ensure that the "Port enable" checkbox is selected, indicating that this element functions as a port. Additionally, make sure that the "Default" checkbox remains unchecked.

Your port configuration is now set up as illustrated in the figure.

![4Asize](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/364f7f20-ba64-49f6-b671-ef1f3635685e)

![5Ysize](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/0498d2e8-80a5-43e2-9731-5bd4c2076a89)

![6VGND](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/0b93e288-eab6-4097-8224-ee5eee2110ce)

![7VPWR](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/2bb3a56c-686b-43eb-9fa9-f9a3858c0e2d)

Open the tkcon window or the relevant environment where you can define port attributes.

Define the purpose of each port as follows:  

```
port A class input
port A use signal

port Y class output
port Y use signal

port VPWR class inout
port VPWR use power

port VGND class inout
port VPWR use ground
```

![8tkconcmd](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/436e3ac6-89b1-43b4-b8c0-b030224eb880)


Generate the lef file using below command:  

``
lef write <name>
``

### Incorporating Custom Cells into OpenLANE Flow

To incorporate the new standard cell into the synthesis process, you should follow these steps:

Begin by duplicating the sky130_vsdinv.lef file and placing it in the designs/picorv32a/src directory.

As ABC maps the standard cell to a specific library, you must ensure that the CMOS inverter is defined within a library. To achieve this, you should copy the sky130_fd_sc_hd_typical.lib file, which is located in the vsdstdcelldesign/libs directory, into the designs/picorv32a/src directory. It's worth noting that you may also need to copy the slow and fast library files if they are relevant to your design. Modify the config.tcl file:  

```

# Design
set ::env(DESIGN_NAME) "picorv32a"

set ::env(VERILOG_FILES) "$::env(DESIGN_DIR)/src/picorv32a.v"

set ::env(CLOCK_PORT) "clk"
set ::env(CLOCK_NET) $::env(CLOCK_PORT)

set ::env(GLB_RESIZER_TIMING_OPTIMIZATIONS) {1}

set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

set filename $::env(DESIGN_DIR)/$::env(PDK)_$::env(STD_CELL_LIBRARY)_config.tcl
if { [file exists $filename] == 1} {
	source $filename
}

```

To seamlessly integrate a standard cell into the OpenLANE flow, execute the following commands:  

```
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```

Below is the synthesis report :  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/8b57cab7-ac7e-4792-adc6-4b15243ae7e5)


### Introduction to Delay tables
In the realm of VLSI design, the parameter of "Delay" wields a profound influence on the behavior of cells within our designs. It essentially acts as the arbiter governing various critical timing aspects. When dealing with cells of different sizes and threshold voltages, we establish what's known as a "delay model table," often referred to as a "timing table." This table plays a pivotal role in capturing the intricate relationship between a cell's delay and its input transition and output load.  

Consider two scenarios: one where a cell (let's call it X1) is situated at the end of a lengthy wire, and another where the same cell is positioned at the terminus of a shorter wire. In the former case, the delay of this cell differs significantly due to the adverse impact of resistance and capacitance along the extended wire, resulting in a slower transition. Conversely, in the latter scenario, with the cell located at the end of the shorter wire, the delay is comparatively lower, reflecting the more favorable signal transition conditions. Even though both instances employ the same cell, the delay is distinctly altered based on the input transition characteristics, illustrating the profound influence of wire length.  

VLSI engineers have discerned a set of specific constraints governing the insertion of buffers to uphold signal integrity. They've observed that each buffer level must adhere to consistent sizing, yet their individual delays can fluctuate contingent upon the load they are driving. To address this intricate challenge, they introduced the concept of "delay tables." These tables essentially manifest as two-dimensional arrays, housing precise values for input slew and load capacitance, each associated with varying buffer sizes. These delay tables serve as comprehensive timing models for our designs.  

In the practical execution of algorithms, these delay tables become indispensable tools. They leverage provided input slew and load capacitance values to dynamically compute the corresponding delay values for the associated buffers. In scenarios where exact delay data may be lacking, the algorithm adeptly employs interpolation techniques. It strategically identifies the nearest available data points within the tables and extrapolates from them to estimate the requisite delay values, ensuring the precision and reliability of the overall design. This method allows VLSI designers to navigate the complex interplay of delay, signal integrity, and buffer management, ultimately delivering optimized and functional semiconductor devices.  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/7feef496-f5ec-4e1c-8714-3bea1e5cd6eb)

### Custom Standard Cell Integration in the OpenLane Flow  

We conducted synthesis and identified negative slack while also successfully meeting the timing constraints.
  
During the floorplan stage, we detected the inclusion of the custom cell.  


Now do ``run_placement``

![skyinv_vsd](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/2f30efae-932e-4e70-94a2-9ee2e4988136)

Here below are other cells :  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/21aa466f-1942-41a1-8d5d-0a2f9fd0795f)




### Setup & Hold time:  

Setup Time is the time the input data signals are stable (either high or low) before the active clock edge occurs. **Hold Time** is the time the input data signals are stable (either high or low) after the active clock edge occurs.  
Below is the representation:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/6867bffd-28f6-4d8a-afd3-a6390018f457)

Lets understand in detail: Setup time is a crucial parameter, signifying the minimum duration preceding the active edge of the clock signal during which the data input must remain steady for accurate latching. Should this requirement be disregarded, it can lead to a perilous scenario known as a setup violation. In such instances, incorrect data may be captured, imperiling the integrity of the entire system.  

Conversely, HOLD time represents another pivotal consideration, specifying the minimum interval post the clock's active edge within which the data input must stay unchanged. A violation in this context results in a hold violation, often culminating in erroneous data latching. It's vital to emphasize that both setup and hold times are exclusively measured concerning the clock's active edge. These stringent timing constraints form the cornerstone of dependable and error-free digital circuit operation, safeguarding against data corruption and ensuring reliable data capture.  

### Clock Jitter:  

It can be defined as “deviation of a clock edge from its ideal location.” Clock jitter is typically caused by clock generator circuitry, noise, power supply variations, interference from nearby circuitry etc. Jitter is a contributing factor to the design margin specified for timing closure.  

Below is the representation :  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/85c916e4-b62c-4249-9097-d26137fa8697)


**Causes of Clock Jitter:**  

 
**Noise:** Electronic circuits can introduce noise, which can cause fluctuations in the clock signal. This noise can come from various sources, such as power supply fluctuations or electromagnetic interference.  

**Component Variations:** Variations in the characteristics of electronic components like resistors, capacitors, and transistors can lead to clock jitter.  

**Temperature Fluctuations:** Changes in temperature can affect the performance of electronic components, leading to jitter.  

**Phase-Locked Loops (PLLs):** PLLs are commonly used to generate stable clock signals, but they can introduce jitter if not designed or configured correctly.  

**Clock Distribution:** As clock signals travel through PCB traces or cables, they can experience delays or reflections, leading to jitter.

### Clock Tree Synthesis 

The primary objective when constructing a clock tree is to ensure the reliable distribution of the clock signal to all elements in the design while minimizing clock skew. One commonly employed method in Clock Tree Synthesis (CTS) is the utilization of the H-tree architecture. If you've previously attempted to address slack issues in a design, you may have observed alterations in the netlist due to cell replacement techniques. Before proceeding with CTS using the TritonCTS tool, it's essential to consider these aspects.  

Clock Tree Synthesis serves the crucial purpose of optimizing the clock signal's routing resources, reducing the area occupied by clock repeaters, and simultaneously adhering to various timing and power specifications. These specifications encompass reasonable clock skew, acceptable clock latency, controlled clock transition times, minimum pulse width, duty cycle adherence for all sequential elements in the design, and maintaining clock power within defined limits. Clock skew, in particular, pertains to the difference in clock arrival times between two registers.  

Importance of Clock Tree Synthesis:  


- In digital ICs, clock signals are fundamental for synchronizing the operation of various components, ensuring that data is sampled or changed at the correct times.

- Properly synchronized clocks are crucial for avoiding setup and hold time violations, which can lead to incorrect data processing.

- As ICs become more complex with millions or even billions of transistors, efficient and reliable clock distribution becomes increasingly challenging.

Below is the representation:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/821bf9ec-2c78-4f5a-95ee-ceef209c859e)

Below shown cts buffering  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/429fd0f9-0f30-40ab-a359-4b9f62ab8472)


### Crosstalk and clock net shielding

Crosstalk refers to an undesirable phenomenon that occurs when signals on adjacent conductors or interconnects interfere with each other. This interference can lead to errors in data transmission and reception, which can ultimately impact the overall functionality and performance of integrated circuits (ICs) and electronic systems. Crosstalk can manifest in both digital and analog circuits and can be a significant concern as ICs become more densely packed with components and interconnects.  

Clock net shielding, also known as clock tree shielding, is a technique used in Very Large Scale Integration (VLSI) design to reduce the impact of crosstalk and noise on clock signals. Clock signals are critical in digital circuits as they synchronize the operation of various components within an integrated circuit (IC). Ensuring the integrity of clock signals is crucial to the overall performance and reliability of the IC.

Below is the representation:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/85ee62a5-e64c-4d3b-9619-41eb2711cf18)


**Types of Crosstalk**:  

- Capacitive Crosstalk: This occurs due to the capacitive coupling between adjacent conductors. When one signal transitions from high to low (or vice versa), it induces a voltage change on nearby conductors, leading to interference.  
- Inductive Crosstalk: This results from the inductive coupling between conductors. When there is a change in current flow in one conductor, it induces a voltage in an adjacent conductor, causing interference.

**Techniques to Mitigate Crosstalk**:

- Spacing and Wire Sizing: Increasing the distance between adjacent conductors and using wider wires can reduce capacitive and inductive coupling.
- Shielding: Adding shielding layers between sensitive conductors can minimize interference.
- Buffering and Repeaters: Buffering signals and inserting repeater circuits can help restore signal integrity.
- Clock Gating: Disabling clock signals when not in use can reduce dynamic power consumption and crosstalk.

### Lab Using TritonCTS:  

In this stage, our primary goal is to ensure that the clock signal propagates uniformly to reach every clock pin from the source while minimizing skew and insertion delay. To achieve this, we employ an H-tree structure using a midpoint strategy. Additionally, to balance any remaining skews, we strategically incorporate clock inverters or buffers along the clock path.  


Before initiating Clock Tree Synthesis (CTS) in TritonCTS, it's important to note that if any previous attempts were made to reduce slack, there may have been modifications to the netlist through cell replacement techniques. Consequently, it's imperative to update the Verilog file using the "write_verilog" command. After this modification, the synthesis, floorplan, and placement steps need to be re-executed.  


To initiate the Clock Tree Synthesis (CTS) process, please use the following command:  

```
run_cts
```

open openroad tool using following in openlane command prompt.  

```
openroad
```
![12](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/334fd5f3-db94-4484-a822-eb73d9ec0b73)

Now give below commands one by one:  

```
read_lef ./designs/picorv32a/runs/RUN_2023.09.16_12.00.29/tmp/merged.nom.lef 
read_def ./designs/picorv32a/runs/RUN_2023.09.16_12.00.29/results/cts/picorv32a.def
write_db ./designs/picorv32a/picorv32a.db
read_verilog ./designs/picorv32a/picorv32a_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
read_sdc ./designs/picorv32a/runs/RUN_2023.09.16_12.00.29/results/cts/picorv32a.sdc
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```

![11](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/8f40f6de-4c0c-401d-986a-48969ab38278)


# Day 5 Final steps for RTL2GDS

### Maze Routing and Lee's algorithm

**The maze-routing algorithm** is a low overhead method to find the way between any two locations of the maze. The algorithm is initially proposed for chip multiprocessors (CMPs) domain and guarantees to work for any grid-based maze.  

Below is the representation:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/3443b6d2-063f-42c6-b8ff-81126a706549)  

**Algorithm Steps:**  

**Initialization:**  

- Create a grid or matrix representation of the routing area, where each cell represents a routing point.
- Mark the source point with a value of 0.
- Initialize all other cells with a large "infinity" value or a high number to represent unexplored areas or obstacles.

**Wavefront Expansion:**
  

- Start with the source point and assign it a value of 0.
- Begin a wavefront expansion process by visiting each point in the grid in a systematic manner (typically in a breadth-first search fashion).
- For each unvisited neighbor of a point with the current wavefront value 'n', assign it a value of 'n+1'. This process continues until the destination point is reached or until no further progress is possible.

**Backtracing:**
  

- Once the destination point is reached, backtrack from the destination to the source by choosing the neighbor with the lowest value at each step.
- This path will represent a valid route from source to destination that avoids obstacles.
  
**Path Extraction:**  


- The backtracing process yields the path from the source to the destination.
- This path can be used as a guide for routing wires or interconnects in the VLSI layout.

 **Limitations:**  
 

- Lee's algorithm may not always find the shortest path, especially if there are multiple paths with the same wavefront values.
- It does not consider congestion or wirelength minimization, which are essential factors in VLSI routing. More advanced routing algorithms are often used for those purposes.

### Design Rule Check

DRC is used to ensure that the physical layout of an integrated circuit (IC) adheres to the manufacturing and design rules specified by the semiconductor fabrication process. These rules are essential to ensure the manufacturability, functionality, and reliability of the IC.  

 Semiconductor foundries or fabrication facilities specify a set of design rules that must be followed for a particular process technology. These rules include guidelines for minimum feature sizes, spacing between components, layer alignments, and other layout parameters.  

 ![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/725c581a-7b50-4848-b0e3-fc6b2c7b0b4c)


![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/87166e1b-f57c-4039-a90f-69b002b8051b)


**DRC Checks**: The DRC tools perform various checks to ensure compliance with design rules, including:  


- Spacing Rules: Ensuring that there is sufficient space between adjacent features to prevent short circuits or manufacturing defects.
- Width Rules: Verifying that the width of conductive traces and other components meets the minimum requirements.
- Alignment Rules: Checking that different layers of the IC align properly to prevent misalignment issues.
- Enclosure Rules: Confirming that certain components are properly enclosed within designated regions.
- Notch Rules: Ensuring that certain features have notches or cutouts as required.
- Via Rules: Checking the size and placement of vias, which connect different layers in the IC.
- Antenna Rules: Verifying that charge buildup and discharge during fabrication are within acceptable limits.

### Power Distribution Network and routing

It is an infrastructure that provides a stable and reliable supply of electrical power to all components within an integrated circuit (IC) or chip. Generating a proper PDN is essential to ensure that all devices on the chip receive the required voltage levels with minimal noise and voltage drops.  

The first step in generating the PDN is to plan the power grid. This involves determining the overall power requirements of the chip, including the voltage levels (typically VDD and VSS or ground) and the current needs of different functional blocks.  

Designers also need to consider the power delivery network's topology, including the placement of power rails and ground lines, as well as the arrangement of power domains and their connectivity.  

To stabilize the voltage and reduce noise, decapacitors (decaps) are strategically placed within the chip. Decaps act as local energy reservoirs and help compensate for sudden changes in current demand, especially during switching events.  

The selection and placement of decaps are based on the expected load and voltage fluctuations in different regions of the chip.  

we can check whether PDN has been created or no by check the current def environment variable:  ```echo $::env(CURRENT_DEF)```  and then ``gen_pdn``  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/0031085e-8a0b-4894-9d04-c8cfdec5b79c)

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/5c430f3c-c9e7-4a15-9b89-0914f768c54c)


Once the PDN is generated, designers use analysis tools to simulate and verify its performance. They check for voltage drop, IR (voltage drop due to resistance), electromigration, and other power-related issues.  

Optimization techniques such as buffer insertion, voltage islands, and voltage scaling may be applied to improve PDN performance.  

After the chip's layout is complete, designers perform post-layout verification to confirm that the actual layout adheres to the PDN plan and design rules. Any discrepancies or issues are addressed.  

Once the PDN is successfully generated and verified, and all design rules are met, the chip design is considered ready for tape-out. The final layout data is sent to a semiconductor foundry for fabrication.

### Routing

It is the process of establishing interconnections between various components (such as transistors, gates, and blocks) within an integrated circuit (IC) to enable proper functionality and data flow. It involves creating a network of wires or metal traces to connect different components according to the logical design and constraints while optimizing for factors like signal integrity, power efficiency, and manufacturability.  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/8468d045-f7fe-4263-b664-b9792e641f59)


**Global vs. Detailed Routing:**  

- Global Routing: This is the initial phase of routing where the major pathways for interconnects are defined. It determines the approximate location of wires and establishes high-level connections.
- Detailed Routing: After global routing, detailed routing focuses on the specific routing paths for each net (a collection of connected components). It involves selecting the exact wires and vias (connections between metal layers) to create a functional and manufacturable layout.

### TritonRoute Features  

 TritonRoute is an open-source routing tool, which means it is freely available for use, modification, and distribution.  

 TritonRoute focuses on detailed routing, which involves the precise placement of wires and vias to connect the various components and nets within an integrated circuit. It is typically used in the later stages of the physical design flow. The tool allows designers to specify the assignment of metal layers for routing, considering factors such as signal speed, power distribution, and available resources. Choosing the appropriate metal layers is essential for optimizing performance.  

 The tool takes into account the placement of standard cells, macro blocks, and other routing tracks as obstacles when determining the path of wires. It avoids collisions and ensures connectivity. TritonRoute employs routing algorithms to find the optimal paths for interconnections. The choice of algorithm can impact factors such as wirelength, signal delay, and power consumption.  

  TritonRoute-generated layouts are subject to physical verification steps to check for manufacturing-related issues, such as design rule violations and DRC errors.

## Acknowledgement
1.  Kunal Ghosh, VSD Corp. Pvt. Ltd.
2.  Alwin shaju,Colleague,IIIT B
3.  Bhargav DV, Colleague, IIIT B
4.  Divyam Satle, Colleague, IIITB

## References
1. https://github.com/The-OpenROAD-Project/OpenLane
2. https://github.com/kunalg123/
3. https://openlane.readthedocs.io/en/latest/getting_started/installation/installation_ubuntu.html#installation-of-required-packages'
4. https://vsdiat.com/
5. https://github.com/Devipriya1921/Physical_Design_Using_OpenLANE_Sky130
6. https://github.com/nickson-jose/vsdstdcelldesign/
7. http://opencircuitdesign.com/magic/
8. https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html
9. https://en.wikipedia.org/
10. https://www.researchgate.net/
