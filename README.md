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
![block dia](https://github.com/sprusty23/SRAM/blob/master/schematics/SRAM.png)


## Bit-cell array(6T cell)
- The 6T cell is the default memory cell because it is the most commonly used cell in SRAM devices. 6T cells are tiled together with abutting word- and bit-lines to make up the memory array. The bit-cell array’s aspect ratio is made as square as possible using multiple columns of data words. The memory cell is a custom designed library cell for each technology. Other types of memory cells, such as 7T, 8T, and 10T cells, can be used as alternatives to the 6T cell.   

### 6T-SRAM Memory cell
 
![SRAM_6t](https://github.com/sprusty23/SRAM/blob/master/schematics/6t.png)

- In this project I have designed and characterised the Bit-cell array of SRAM-6T cell using NGSpice tool with 0.5um SCMOS technology from MOSIS.
  
- In this section I have represented the DC analysis and Transient Analysis of the 6T-SRAM cell which I have simulated using NGSpice

**DC Analysis**
  
  ![Dc sim](https://user-images.githubusercontent.com/71965706/94514148-1cd6d000-023e-11eb-8fc0-00866ce9f399.png)
- From the Dc Analysis we get the operating point of the CMOS Inverters at the intersection of input and output voltage.
 - we also get the Design Margin for the pull-up and pull-down device by performing write operatrion.

#DC corner simulation data:
 ![DC sim](https://github.com/sprusty23/SRAM/blob/master/schematics/dc_table.png )

- I have simulate the cicuit at different corner (Slow slow, fast fast, Nominal) at 3 different temperature and found that at slow slow 120°C temperature it shows worst result.

![DC analysis](https://github.com/sprusty23/SRAM/blob/master/schematics/dc_plot.png)
- This is the plot of word line, the stored data Q and Qbar. 

  **Transient Analysis**
  ![SRAM_sim](https://github.com/sprusty23/SRAM/blob/master/schematics/transi_table.png)
  
In the above simulation i have done a Write-Read-write operation. I have calculated the maximum volatages variation at internal node for the
 
  **Simulation Result**
  
  ![SRAM](https://github.com/sprusty23/SRAM/blob/master/schematics/transient.png)


 
  
 ## Circuit Daigram of SRAM cell with all Parasitcs**
 
 ![sram_parasitics](https://github.com/sprusty23/SRAM/blob/0ba994ce0b57662f6ac72ef77f38e4181ec6abfb/schematics/parasitics.png)

##Precharge Circuit
- This circuitry pre-charges the bit- lines during the first phase of the clock for read operations.
The precharge circuit is placed on top of every column in the memory array and equalizes the bit-line voltages so that the sense amplifier can sense the voltage difference between the two bit-lines.

- In the above circuit diagram the M5, M6, M7 mosfets are used for pre-charging the Bit and Bit bar line. M8 and M9 mosfets are used at the time of write operation. As 1k 32-bit SRAM consists of 32k of bit cells, so it can taken as 128*256(i.e. 128 number of rows and 256 number of columns). For Simulation we are taking one 6T SRAM cell with the parasitic capacitor of all the cells. cw1 ,cw2 ,cw3 are the wire load capacitors(10fF/cell) which are connected to bit, complementary bit and word line. Simillarly M1, M2, M3, M4 are the parasitic mosfets whose total capacitance is equal to the 1k 32-bit cell array.
### Sense Amlifier
- A differential sense amplifier is used to sense the voltage difference between the bit-lines of a memory cell while a read operation is performed. The sense amplifier uses a bit-line isolation technique to increase per-
              formance. The sense amplifier circuitry is placed below thecolumn multiplexer or the memory array if no              column mul- tiplexer is used. There is one sense amplifier for each output bit.
- 
Sense Amplifier generally used to detect the node voltage stored in the memory. It will be on at the time of Read operation. I have used a latch based Sense amplifier in my design.
  
  **Circuit Diagram**
![Sense_amp](https://github.com/sprusty23/SRAM/blob/master/schematics/sense_amp.png) 
  
### Write Driver 
- The write drivers send the input data signals onto the bit-lines for a write operation. The write
drivers are tri-stated so that they can be placed between the column multiplexer/memory array and the sense amplifiers.
- There is one write driver for each input data bit.

- The write drivers send the input data signals onto the bit-lines for a write operation. The write drivers are tri-stated so that they can be placed between the column multiplexer/memory array and the sense amplifiers. There is one write driver for each input data bit.

**Circuit Diagram**

![write_driver](https://user-images.githubusercontent.com/71965706/94522716-b48fea80-024d-11eb-8e7a-538e793c3781.png)

## Simulation of 6T-SRAM cell with write driver and sense amplifier

![clksync](https://github.com/sprusty23/SRAM/blob/master/schematics/Write_pulse.png)

### Installing and Simulating on NGSpice
To Download NGSpice on your System
**Clone the Repo**
'git clone https://www.github.com/silicon-vlsi/project2020'


## Future work
- To create the layout using Magic.
- And to compile the whole circuit using the OpenRAM compiler. 

  


