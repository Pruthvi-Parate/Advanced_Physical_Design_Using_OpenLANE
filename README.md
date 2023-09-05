# Advanced_Physical_Design_Using_OpenLANE

## Table of Contents
**1. Day 1**
-  [How to talk to computers ](#how-to-talk-to-computers)
- [Introduction to RISCV ](#introduction-to-RISCV--)
-    [From Software Applications to Hardware](#from-software-applications-to-hardware--)

**2. Day 2**
- [Good and Bad Floorplanning , Placement and library cells](#day-2--good-and-bad-floorplanning--placement-and-library-cells)



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

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/686d8a71-a016-4b77-83b2-2b3625f4cf91)

Below is synthesis_pre report:  

![image](https://github.com/Pruthvi-Parate/Advanced_Physical_Design_Using_OpenLANE/assets/72121158/f73e82ad-a3bd-4a95-aa71-8542b4f47ebd)


# DAY 2 : Good and Bad Floorplanning , Placement and library cells



## References
1. https://github.com/The-OpenROAD-Project/OpenLane
2. https://github.com/kunalg123/
3. https://openlane.readthedocs.io/en/latest/getting_started/installation/installation_ubuntu.html#installation-of-required-packages
4. https://en.wikipedia.org/
