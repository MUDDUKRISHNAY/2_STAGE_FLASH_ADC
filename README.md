# 4_bit_2_STAGE_FLASH_FLASH_ADC
Analog  to digital converter  to reduce area and quantization error 

#Abstract
This project presents the design and implementation of a 2-Stage Flash Analog-to-Digital Converter (ADC), an optimized architecture aimed at reducing power consumption, chip area, and comparator count while maintaining high-speed conversion.
A conventional n-bit Flash ADC requires (2^(𝑛))−1 comparators, resulting in high power and area overhead, especially for higher resolutions. The 2-Stage Flash ADC, also known as a subranging ADC, overcomes this limitation by dividing the conversion process into two stages:
Stage 1 performs a coarse conversion to resolve the Most Significant Bits (MSBs).
Stage 2 converts the residue (the difference between the input and DAC-reconstructed signal from Stage 1) to obtain the Least Significant Bits (LSBs).


Flash ADC 
Structure: Single-stage ADC.
Number of Comparators:
(2^(𝑛))−1 comparators for n-bit resolution 
For example, a 4-bit flash ADC requires 15 comparators.

Two-Stage Flash ADC 
Structure: Two stages – coarse and fine.
Number of Comparators:
Reduced significantly compared to flash ADC.
For an n-bit ADC split into k-bit coarse and (n−k)-bit fine:
(2^(k)−1)+(2^(n−k)−1) comparators
Example: 4-bit ADC split into 2+2 : (2^(2)−1) + (2^(2)−1) = 3+3 = 6 comparators 

This architecture significantly reduces the total number of comparators and allows high-speed conversion with improved efficiency. The project includes schematic design, simulation results, and system-level analysis demonstrating the performance advantages of the 2-Stage Flash ADC.

# Architecture of 4_bit_2_stage_flash_adc
![image](https://github.com/user-attachments/assets/4571d8f8-0248-49f4-86d3-97f4146b4961)

# different Blocks used in this Architecture are:
1  sample and hold 
2  flash ADC
3  DAC (c2c DAC)
4  subtractor
5  residue_Amplifier


I used OPAMP in sample and hold circut , subtractor circuit and residue_Amplifier
In Flash ADC I used :
1 comparator
2 Thermometer to Binary encoder

In DAC (c2c DAC) I used
1 Switch

