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




## References
1. https://github.com/The-OpenROAD-Project/OpenLane
2. https://github.com/kunalg123/
3. https://openlane.readthedocs.io/en/latest/getting_started/installation/installation_ubuntu.html#installation-of-required-packages
4. https://en.wikipedia.org/
5. https://www.researchgate.net/
