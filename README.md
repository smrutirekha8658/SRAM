# CMOS SRAM IP in MOSIS 0.5µm CMOS technology.

##  What is SRAM ?
   SRAM (static RAM) is random access memory  that retains data bits in its memory as long as power is being supplied. SRAM does not have to be periodically refreshed. Static RAM provides faster access to data and is more expensive than DRAM. 
We can design SRAM in many ways based on number of transistor used in its core cell. For example : 6T SRAM, 8T SRAM, 9T SRAM etc..


## CONTENTS
 - SRAM Design 
 - Block Diagram of SRAM cell
 - Standard 6T SRAM Cell
 	-  Custom Cells
	-  DC Simulation
	-  Static Noise Margin
		- RNM (Read Noise Margin)
		- WNM (Write Noise Margin)
	- Prelayout Simulation
	-Layout
 - Comparitive Study of  6T , 8T, 9T SRAM cells 
	- 8transistor SRAM cell
		- Block Diagram
		- Static Noise Margin
			- RNM (Read Noise Margin)
			- WNM(Write Noise Margin)
		- Prelayout Simulation
		- Layout
	- 9transistor SRAM cell
		- Block Diagram
		- Static Noise Margin
			- RNM (Read Noise Margin)
			- WNM(Write Noise Margin)
		- Prelayout Simulation
		- Layout
	- Comparison based  on
       - Noise Margin
       - Area
       - Parasitic Capacitance
- Future Work
- Acknowledgement

## SRAM specification   
 - Memory Size                -       1k * 32-bit. 
 - Operating voltage         -       5V
 - Technology  PDK file  -       0.5µm CMOS Technology
 - Access Time                 -       < 30 ns
 - Tools Used                   -       Sue2 ,  NGSpice  ,  Magic
 - Compiler                      -       Open source memory compiler OpenRAM. (https://github.com/mguthaus/OpenRAM/blob/master/OpenRAM_ICCAD_2016_paper.pdf "OpenRAM")

## Block Diagram of  SRAM 
![block dia](https://github.com/sprusty23/SRAM/blob/master/schematics/SRAM.png)
 
## Standard 6T SRAM design Blocks 
 The SRAM block consists of 8 major blocks :
- Bit-cell array
- Precharge Circuit
- Sense Amplifier
- Write Driver
- Word-line driver 
-  Control logic 
-  Column Multiplexer
-  Address Decoder

## Bit-cell array(6T cell)
- The 6T cell is the default memory cell because it is the most commonly used cell in SRAM devices. 6T cells are tiled together with abutting word- and bit-lines to make up the memory array. The bit-cell array’s aspect ratio is made as square as possible using multiple columns of data words. The memory cell is a custom designed library cell for each technology. Other types of memory cells, such as 7T, 8T, and 10T cells, can be used as alternatives to the 6T cell.   

### 6T-SRAM Memory cell
 
![SRAM_6t](https://github.com/sprusty23/SRAM/blob/master/schematics/6t.png)

## DC Analysis
  
  ![Dc sim](https://user-images.githubusercontent.com/71965706/94514148-1cd6d000-023e-11eb-8fc0-00866ce9f399.png).

## DC corner simulation data:
 ![DC sim](https://github.com/sprusty23/SRAM/blob/master/schematics/dc_table.png )
  
## Circuit Daigram of SRAM cell with all Parasitcs**
 
![sram_parasitics](https://github.com/sprusty23/SRAM/blob/0ba994ce0b57662f6ac72ef77f38e4181ec6abfb/schematics/parasitics.png)

### Precharge Circuit
- This circuitry pre-charges the bit- lines during the first phase of the clock for read operations.
The precharge circuit is placed on top of every column in the memory array and equalizes the bit-line voltages so that the sense amplifier can sense the voltage difference between the two bit-lines.


### Sense Amlifier
- A differential sense amplifier is used to sense the voltage difference between the bit-lines of a memory cell while a read operation is performed. The sense amplifier uses a bit-line isolation technique to increase performance.

  ![Sense_amp](https://github.com/sprusty23/SRAM/blob/master/schematics/sense_amp.png) 
  
### Write Driver 
- The write drivers send the input data signals onto the bit-lines for a write operation. The write
drivers are tri-stated so that they can be placed between the column multiplexer/memory array and the sense amplifiers.
- There is one write driver for each input data bit. - The write drivers send the input data signals onto the bit-lines for a write operation. The write drivers are tri-stated so that they can be placed between the column multiplexer/memory array and the sense amplifiers. There is one write driver for each input data bit.

**Circuit Diagram**

![write_driver](https://user-images.githubusercontent.com/71965706/94522716-b48fea80-024d-11eb-8e7a-538e793c3781.png)


## 6T cell Stability

### RNM (Read Noise Margin)
![RNM](https://github.com/sprusty23/SRAM/blob/master/schematics/RNM_6T.png)

### WNM (Write Noise Margin)
![WNM](https://github.com/sprusty23/SRAM/blob/master/schematics/wnm_6tt.png)

## Prelayout  Simulation
![clksync](https://github.com/sprusty23/SRAM/blob/master/schematics/Write_pulse.png)
  

 ## Corner Simulation
  ![SRAM](https://github.com/sprusty23/SRAM/blob/master/schematics/transi_table.png)

## 6T-SRAM Memory cell Layout
![6t_layout](https://github.com/sprusty23/SRAM/blob/master/schematics/6t_layout.png)


# A Comparative Study of 6Transistor ,  8Transistor and 9Transistor SRAM Cell

### 8T SRAM Memory Cell
Basic Structure:
 Each bit in a 8T SRAM requires 8transistors. Two NMOS pass transistors for Read and Write
operations which are also known as access transistors. Four transistors for the two-inverter latch and two transistors for an inverter for read operation. From below fig M5 and M6 are the access transistors, M1, M2, M3 and M4 are the transistors for two inverter latch and M7 and M8 are the transistors for the read operation. The Bit line as well as the Read word line and Write word line are connected to the access transistors
for Read and Write on the latch.

## Circuit Diagram
![8tcell]( https://github.com/sprusty23/SRAM/blob/master/schematics/8t.png)


## RNM (Read Noise Margin)
![RNM](https://github.com/sprusty23/SRAM/blob/master/schematics/RNM_8T.png)

## WNM(Write Noise Margin)
![WNM](https://github.com/sprusty23/SRAM/blob/master/schematics/WNM_8T.png)

## Layout
![layout](https://github.com/sprusty23/SRAM/blob/master/schematics/8t_layout.png)

### 9T SRAM Memory Cell
Basic Structure: Each bit in a 9T SRAM requires 9transistors. Two NMOS pass transistors for Write operation which are also known as access transistors. Four transistors for the two-inverter latch, three transistors for read operation. From below Fig M5 and M6 are the access transistors, M1, M2,
M3 and M4 are the transistors for two inverter latch and M7, M8 and M9 are the transistors for the read operation. The Bit line as well as the Read word line and Write word line are
connected to M9 and the access transistors for Read and Write on the latch respectively.

## Circuit Diagram
![9tcell]( https://github.com/sprusty23/SRAM/blob/master/schematics/9t.png)


## RNM (Read Noise Margin)
![RNM](https://github.com/sprusty23/SRAM/blob/master/schematics/RNM_8T.png)

## WNM(Write Noise Margin)
![WNM](https://github.com/sprusty23/SRAM/blob/master/schematics/wnm_6tt.png)

## Layout
![layout](https://github.com/sprusty23/SRAM/blob/master/schematics/9t_layout.png)

## Comparison Based On
### Read Noise Margin
![rnm](https://github.com/sprusty23/SRAM/blob/master/schematics/RNM_Table.png)

###  Write Noise Margin
![rnm](https://github.com/sprusty23/SRAM/blob/master/schematics/WNM_table.png)

### Area and Parasitics
![rnm](https://github.com/sprusty23/SRAM/blob/master/schematics/area_table.png)






### Conclusion
- Different configurations of SRAM transistor have been compared. The 6T SRAM provide very less RNM which is further degraded due to process variation. 
- To obtain higher RNM in 6T SRAM cell width of the pull down transistor has to be increased but this increases area of the SRAM which in turn increases the leakage currents.
- The 8T SRAM cell provide higher read noise margin and its area is also small but its WNM is very small. Hence it is more prone to failure during write operation. Besides this the cell is not symmetric and its write time is also higher.
- On the other hand 9T SRAM cell has higher RNM as well as WNM and its write time is also small. The leakage current of 9T SRAM cell is reduced by using dual threshold voltage technology. 

### Acknowledgement
- Dr. Saroj Rout, Associate Professor, Silicon Institute Of Technology
- Mr.Santanu Srangi, Assistant Proffesor, Silicon Institute of Technology


