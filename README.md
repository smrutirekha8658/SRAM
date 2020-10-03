# CMOS SRAM IP in MOSIS 0.5µm CMOS technology.

##  What is SRAM ?
   SRAM (static RAM) is random access memory  that retains data bits in its memory as long as power is being supplied. SRAM does not have to be periodically refreshed. Static RAM provides faster access to data and is more expensive than DRAM. 
We can design SRAM in many ways based on number of transistor used in its core cell. For example : 6T SRAM, 8T SRAM, 9T SRAM etc..
This project is focused on  6T SRAM memory design.

##SRAM specification   
- Memory Size -  1k * 32-bit. 
- Operating voltage - 5V
- Technology  PDK file - 0.5µm CMOS Technology
- Tool Used – Sue2, NGspice,  Magic
- Compiler – Open source memory compiler OpenRAM. (https://github.com/mguthaus/OpenRAM/blob/master/OpenRAM_ICCAD_2016_paper.pdf "OpenRAM")
 
## SRAM Design 
 The SRAM block consists of 8 major blocks:
- Bit-cell array
- Precharge Circuit
   -  Sense Amplifier
   -  Write Driver
   -  Word-line driver 
   -  Control logic 
   -  Column Multiplexer
   -  Address Decoder

    
 ## Block Diagram
![block dia](https://user-images.githubusercontent.com/71965706/94511998-881da380-0238-11eb-91c3-ffe9e7b702da.png)


## Bit-cell array(6T cell)
- The 6T cell is the default memory cell because it is the most commonly used cell in SRAM devices. 6T cells are tiled together with abutting word- and bit-lines to make up the memory array. The bit-cell array’s aspect ratio is made as square as possible using multiple columns of data words. The memory cell is a custom designed library cell for each technology. Other types of memory cells, such as 7T, 8T, and 10T cells, can be used as alternatives to the 6T cell.   

### 6T-SRAM Memory cell
  **Circuit Diagram**
![SRAM_6t](https://user-images.githubusercontent.com/71965706/94513996-b6ea4880-023d-11eb-81be-3733cea20c55.png)

- In this project I have designed and characterised the Bit-cell array of SRAM-6T cell using NGSpice tool with 0.5um SCMOS technology from MOSIS.
  
- In this section I have represented the DC analysis and Transient Analysis of the 6T-SRAM cell which I have simulated using NGSpice

-  **DC Analysis**
  
  ![Dc sim](https://user-images.githubusercontent.com/71965706/94514148-1cd6d000-023e-11eb-8fc0-00866ce9f399.png)

 - From the Dc Analysis we get the operating point of the CMOS Inverters at the intersection of input and output voltage.
 - we also get the Design Margin for the pull-up and pull-down device by performing write operatrion.

  **Transient Analysis**
  
  ![SRAM_sim](https://user-images.githubusercontent.com/71965706/94520666-472e8a80-024a-11eb-9492-f35dc69cfd40.png)
  
In the above simulation i have done a Write-Read-write operation. Red one is my input signal to Pre-charge circuit. Blue colur represents the word line signal , next 2 signals represents the bit and complemet bit signal and last two signals represents the internal node volatages which stored in the cell.
    I have calculated the maximum volatages variation at internal node for the [PVT](https://in.search.yahoo.com/search?fr=mcafee&type=D210IN662G0&p=pvt+corner+in+vlsi) corners and for the temperature -40C,25C and 105C.
    
  **Simulation Result**
  
  ![SRAM](https://user-images.githubusercontent.com/71965706/94521572-e99b3d80-024b-11eb-967b-eef5a0cfa152.png)


 
  
 # Circuit Daigram of SRAM cell with all Parasitcs**
  
  ![sram_parasitcs](https://user-images.githubusercontent.com/71965706/94519493-3715ab80-0248-11eb-9020-a3098cc748f5.png)
 ![sram_parasitics](https://github.com/sprusty23/SRAM/blob/0ba994ce0b57662f6ac72ef77f38e4181ec6abfb/schematics/parasitics.png)

#Precharge Circuit
- This circuitry pre-charges the bit- lines during the first phase of the clock for read operations.
The precharge circuit is placed on top of every column in the memory array and equalizes the bit-line voltages so that the sense amplifier can sense the voltage difference between the two bit-lines.

- In the above circuit diagram the M1, M2 mosfets are used for pre-charging the Bit and Bit bar line.	While M3 mosfet is used for  M4 and M5 mosfets are used at the time of write operation. As 1k 32-bit SRAM consists of 32k of bit cells, so it can taken as 128*256(i.e. 128 number of rows and 256 number of columns). For Simulation we are taking one 6T SRAM cell with the parasitic capacitor of all the cells. cw1 ,cw2 ,cw3 are the wire load capacitors(10fF/cell) which are connected to bit, complementary bit and word line. Simillarly M6, M7, M8, M9 are the parasitic mosfets whose total capacitance is equal to the 1k 32-bit cell array.
### Sense Amlifier
- A differential sense amplifier is used to sense the voltage difference between the bit-lines of a memory cell while a read operation is performed. The sense amplifier uses a bit-line isolation technique to increase per-
formance. The sense amplifier circuitry is placed below thecolumn multiplexer or the memory array if no column mul- tiplexer is used. There is one sense amplifier for each output bit.
- 
Sense Amplifier generally used to detect the node voltage stored in the memory. It will be on at the time of Read operation. I have used a latch based Sense amplifier in my design.
  
  **Circuit Diagram**
   
   
![Sense](https://user-images.githubusercontent.com/71965706/94522258-ff5d3280-024c-11eb-9a69-a9c65f69bedb.png)
  
### Write Driver
- The write drivers send the input data signals onto the bit-lines for a write operation. The write
drivers are tri-stated so that they can be placed between the column multiplexer/memory array and the sense amplifiers.
- There is one write driver for each input data bit.

- The write drivers send the input data signals onto the bit-lines for a write operation. The write drivers are tri-stated so that they can be placed between the column multiplexer/memory array and the sense amplifiers. There is one write driver for each input data bit.

**Circuit Diagram**

![write_driver](https://user-images.githubusercontent.com/71965706/94522716-b48fea80-024d-11eb-8e7a-538e793c3781.png)

## Simulation of 6T-SRAM cell with write driver and sense amplifier

![clk sync](https://user-images.githubusercontent.com/71965706/94522882-fae54980-024d-11eb-91bf-f5a0534491ce.png)

### Installing and Simulating on NGSpice
To Download NGSpice on your System
**Clone the Repo**
'git clone https://www.github.com/silicon-vlsi/project2020'


## Future work
- To create the layout using Magic.
- And to compile the whole circuit using the OpenRAM compiler. 

  


