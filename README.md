# Advanced_Physical_Design_Using_OpenLANE

## Table of Contents
1. Day 1
-  [How to talk to computers ](#how-to-talk-to-computers)
- [Introduction to RISCV ](#introduction-to-RISCV--)
-    [From Software Applications to Hardware](#from-software-applications-to-hardware--)



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



## References
1. https://github.com/The-OpenROAD-Project/OpenLane
2. https://github.com/kunalg123/
3. https://openlane.readthedocs.io/en/latest/getting_started/installation/installation_ubuntu.html#installation-of-required-packages
4. https://en.wikipedia.org/
