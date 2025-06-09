# 4bit_2_STAGE_FLASH_ADC
Analog  to digital converter  to reduce area and quantization error 

# Abstract
- This project presents the design and implementation of a 2-Stage Flash Analog-to-Digital Converter (ADC), an optimized architecture aimed at reducing power consumption, chip area, and comparator count while maintaining high-speed conversion.

- I am using gpdk90 for this project

- A conventional n-bit Flash ADC requires (2^(𝑛))−1 comparators, resulting in high power and area overhead, especially for higher resolutions. The 2-Stage Flash ADC, also known as a subranging ADC, overcomes this limitation by dividing the conversion process into two stages:
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
- sample and hold 
- flash ADC
- DAC (c2c DAC)
- subtractor
- residue_Amplifier

In sample and hold ,subtractor and residue_Amplifier I used :
- OPAMP

In Flash ADC I used :
- comparator
- Thermometer to Binary encoder

In DAC (c2c DAC) I used:
- Switch

# OPAMP
I used OPAMP which is  in the repository , named OPAMP
- [OPAMP](https://github.com/MUDDUKRISHNAY/OPAMP.git)

# Comparator
- In this project I used static Comparator
- It as Minimum Resolution of 40m V ( which means comparator can detect a minimum voltage difference of 40 millivolts between its two input terminals (V+ and V-) and reliably determine which one is larger)
  
- Comparator circuit
  ![image](https://github.com/user-attachments/assets/07a713c0-c2f5-472e-a3d5-4130ecb68ec6)
  
  Pre amplifier stage :
  - it is like differential amplifier , Amplifies the small input differential voltage (difference between Vin+ and Vin-) before passing it to the next stage.
  - It improves offset and noise performance by amplifying the signal above noise floor and internal offsets.
  - Reduces kickback noise from the latch(Judgment) stage from feeding back to the input source and Provides isolation between the latch and sensitive analog input.
    
 Latch(Judgment) stage :
  - Acts as a high-gain, positive-feedback decision circuit — provides fast, digital-like decision.
  - Converts the analog signal to a sharp digital output (not in full swing).
    
  Output(buffer stage) :
  - Provides drive strength to interface with the next stage.
  - Prevents loading effects on the latch, ensuring it operates fast
  

- Proposed circuit
  ![comparator](https://github.com/user-attachments/assets/d297382d-cc8b-42e4-8e5d-d3dd69825e1b)






