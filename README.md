# 4bit_2_STAGE_FLASH_ADC
Analog  to digital converter  to reduce Area and Quantization error 

- 1.[Abstract](#Abstract)
- 2.[Architecture of 4_bit_2_stage_flash_adc](#Architecture-of-4_bit_2_stage_flash_adc)
- 3.[Different Blocks used in this Architecture](#Different-Blocks-used-in-this-Architecture)
- 4.[Pre Layout Design and simulation](#Pre-Layout-Design-and-simulation)
  - 1.[OPAMP](#OPAMP)
  - 2.[Comparator](#Comparator)
  - 3.[Thermometer To Binary encoder](#Thermometer-To-Binary-encoder)
  - 4.[Two bit Flash ADC](#Two-bit-Flash-ADC)
  - 5.[Sample and Hold ](#Sample-and-Hold )
  - 6.[Subtractor](#Subtractor)
  - 7.[Residue_Amplifier](#Residue_Amplifier)
  - 8.[Switch](#Switch )
  - 9.[Two_bit DAC ](#Two_bit-DAC )
  - 10.[4 bit 2 stage Flash ADC](#4-bit-2-stage-Flash-ADC)

# Abstract
- This project presents the design and implementation of a 2-Stage Flash Analog-to-Digital Converter (ADC), an optimized architecture aimed at reducing power consumption, chip area, and comparator count while maintaining high-speed conversion.

- I am using gpdk90 for this project

- A conventional n-bit Flash ADC requires (2^(𝑛))−1 comparators, resulting in high power and area overhead, especially for higher resolutions. The 2-Stage Flash ADC, also known as a subranging ADC, overcomes this limitation by dividing the conversion process into two stages:
Stage 1 performs a coarse conversion to resolve the Most Significant Bits (MSBs).
Stage 2 converts the residue (the difference between the input and DAC-reconstructed signal from Stage 1) to obtain the Least Significant Bits (LSBs).


Flash ADC 
- Structure: Single-stage ADC.
- Number of Comparators:
- (2^(𝑛))−1 comparators for n-bit resolution
- For example: a 4-bit flash ADC requires 15 comparators.

Two-Stage Flash ADC 
- Structure: Two stages – coarse and fine.
- Number of Comparators:
- Reduced significantly compared to flash ADC.
- For an n-bit ADC split into k-bit coarse and (n−k)-bit fine:
- (2^(k)−1)+(2^(n−k)−1) comparators
- Example: 4-bit ADC split into 2+2 : (2^(2)−1) + (2^(2)−1) = 3+3 = 6 comparators 

This architecture significantly reduces the total number of comparators and allows high-speed conversion with improved efficiency. The project includes schematic design, simulation results, and system-level analysis demonstrating the performance advantages of the 2-Stage Flash ADC.

# Architecture of 4_bit_2_stage_flash_adc
![image](https://github.com/user-attachments/assets/4571d8f8-0248-49f4-86d3-97f4146b4961)

# Different Blocks used in this Architecture
- Sample and hold 
- Flash ADC
- DAC (c2c DAC)
- Subtractor
- Residue_Amplifier

In sample and hold ,subtractor and residue_Amplifier I used :
- OPAMP

In Flash ADC I used :
- comparator
- Thermometer to Binary encoder

In DAC (c2c DAC) I used:
- Switch
# Pre Layout Design and simulation
- In this part we work on design and getting proper output
  
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
- Converts the analog signal to a sharp digital output (non full swing).
    
Output(buffer stage) :
- Provides drive strength to interface with the next stage.
- Prevents loading effects on the latch, ensuring it operates fast
  

- Proposed circuit
  ![comparator](https://github.com/user-attachments/assets/d297382d-cc8b-42e4-8e5d-d3dd69825e1b)

- Testbench for Comparator
  ![image](https://github.com/user-attachments/assets/788ecbfb-f38d-4fd4-aabb-aade84875e8b)

- output of Comparator
  ![image](https://github.com/user-attachments/assets/bc79733d-7805-4f1b-8821-f6d7acbf0915)

# Thermometer To Binary encoder
- In Flash ADC we use 3 Comparator , the Digital output of Comparator is thermometer code which is ( not compact and not in standard binary format) so we use Thermometer To Binary encoder

- Thermometer To Binary encoder circuit
![thermometer_to_binary](https://github.com/user-attachments/assets/2ce12e67-02c5-4af4-8fce-fb98166bb7d2)

- Testbench for Thermometer To Binary encoder
![tm_to_bi_testbench](https://github.com/user-attachments/assets/e52df53e-db2f-40fa-aa80-083a0080672b)

- Output of Thermometer To Binary encoder
![tm_to_bi_output](https://github.com/user-attachments/assets/d5f4626e-e724-404e-af4c-5f9c85d2a086)

# Two bit Flash ADC
- A Flash Analog-to-Digital Converter (Flash ADC) is one of the fastest types of ADC architectures. It uses a 3 comparators to simultaneously compare the input analog voltage against a set of reference voltages.
- The outputs of these comparators form a thermometer code, which is then converted to a binary code using a thermometer-to-binary encoder.

- Flash ADC circuit using Comparator and Thermometer To Binary encoder
  ![image](https://github.com/user-attachments/assets/52bb98d0-cd4a-4d5d-88fd-9f871f3d5323)

- Testbench for Flash ADC
  ![flash-adc_testbench](https://github.com/user-attachments/assets/a090c04f-35bb-492b-94f6-c98f5c9f4ee6)

- Output of Flash ADC
  ![flash_adc_output](https://github.com/user-attachments/assets/d6b8aa3a-2e50-422a-8b76-c01016f92f6f)

# Sample and Hold 
- The Sample and Hold (S/H) circuit is used to capture the input voltage and keep it constant while the ADC is converting the signal.

- Sample and Hold circuit
  ![sampl_and_hold](https://github.com/user-attachments/assets/65a261bc-f528-4722-a1cd-12e47d7a97f8)
  The OPAMP in the above picture is used as Buffer , to reduce Loading effect

- Testbench for Sample and Hold
  ![sample_and_hold_testbench](https://github.com/user-attachments/assets/cfefd6be-acf3-4066-9fcf-67433d5c1c4c)

- Output of Sample and Hold
  ![sample_and_hold_output](https://github.com/user-attachments/assets/811fe102-36cc-45b0-b5c7-66182960950e)

# Subtractor
- In a 2-stage Flash ADC, the subtractor is used to calculate the residue for the second stage.
- After the first stage (coarse ADC) converts the most significant bits (MSBs), its output is converted back to an analog voltage by a DAC.
    
The subtractor then computes:
- Residue = Vin − Vdac

- This residue represents the part of the input that was not captured by the first stage. It is sent to the second stage (fine ADC) to resolve the lower bits (LSBs), improving overall resolution and accuracy.
- This we reduced Quantization error

- Subtractor circuit
![subtractor](https://github.com/user-attachments/assets/33995c52-8b6e-43f5-8283-7a90dd4c1794)

- Testbench for Subtractor
![subtractor_testbench](https://github.com/user-attachments/assets/ca973885-0586-4cc8-8294-41d87f817520)

- Output of Subtractor
![subtractor_output](https://github.com/user-attachments/assets/db1d0610-d512-4b13-bc9c-4d9e9aef5462)
In above picture Vout = v(+) - v(-)

# Residue_Amplifier
- The residue amplifier amplifies the residue voltage coming from the subtractor before it is processed by the second stage ADC.
- This ensures that the full input range is effectively used by the second stage.
- Residue Amplifier gain = 2^(N/2) 
- N -> total number of bits
- The first stage resolves n bits → 2ⁿ levels.
- After the first stage, the maximum possible residue is about 1 LSB of first stage.
- 1 LSB of first stage = Vref / 2ⁿ

Second stage to cover this range using its own (N − n) bits, you need to scale the residue up.
- both stages are designed to have similar resolution → split evenly.
- Total N bits, n = N/2 bits in each stage.
- Multiply the residue by 2ⁿ/2 = 2^(n/2) to stretch it across full-scale input of the second stage.

- Residue_Amplifier circuit
![residue_amplifier](https://github.com/user-attachments/assets/9154e570-5a7b-482d-8218-73a2ec45a26f)
Gain = 1 + (R1/R2) => (1 + (6/2))

- Testbench for Residue_Amplifier
![residue_amplifier_testbench](https://github.com/user-attachments/assets/eaf6f7d0-b318-4f86-b1b2-5cf5187f3e14)

- Output of Residue_Amplifier
![residue_amplifier_output](https://github.com/user-attachments/assets/0bf0c0c6-b8af-475b-ba22-9facf86c17a2)

# Switch 
- Switches are used to switch the output voltage in between Vdd and GND based on the digital bits.
![switch](https://github.com/user-attachments/assets/f0210971-dcda-4a25-a22e-99a371fe22f1)
DAC switches take the digital bits as inputs and switch the output voltage in between Vref and GND. If the digital bit is ‘1’ then M1 and M2 transistors will be ON, transistors M3 and M4 will be OFF. This makes the switch output raise to Vdd. If the digital bit is ‘0’ then M3 and M4 transistors will be ON, transistors M1 and M2 will be OFF. This makes the switch output fall to ground voltage.
- The part in red circle VREFH( Reference voltage High) = 1.3 V
- The part in green circle is VREFL( Reference Voltage Low ) = 0 V

- proposed Circuit
![SWITCH](https://github.com/user-attachments/assets/c0ace540-9712-444e-8691-9a7317b818cd)
As seen in Schematic, digital inputs are the control terminals to the switches of a DAC. Switches are used to switch the output voltage in between Vdd and GND based on the digital bits.

- Testbench for Switch
![switch_testbench](https://github.com/user-attachments/assets/9209493c-15f1-4ce5-a340-a2b1c6a0c0fa)

- Output of Switch
![Switch_output](https://github.com/user-attachments/assets/14c606e5-1e71-4918-95e1-e1b8853b030f)

# Two_bit DAC 
- A C2C DAC is a type of capacitive Digital-to-Analog Converter that uses a network of capacitors instead of resistors to perform digital-to-analog conversion.
- Each bit of the digital input controls a capacitor switch connected to either reference voltage (Vref) or ground.
- The network of capacitors forms a charge divider, and the combined charge determines the analog output voltage.

- Two_bit DAC Circuit 
![DAC](https://github.com/user-attachments/assets/f1319bc0-115c-4cc7-af32-18979256ce87)

- Testbench for Two_bit DAC
![DAC_testbench](https://github.com/user-attachments/assets/3d7de32b-ee82-4c35-8e6b-d26ff6690a2a)

- Output of Two_bit DAC
![switch_output](https://github.com/user-attachments/assets/678ab290-9a67-428b-b0b7-0055f0774c23)

# 4 bit 2 stage Flash ADC
- By Integrating all above mentioned blocks we can get full structure 4 bit 2 stage Flash ADC

- Proposed circuit
![2_stage_flash_adc_sh](https://github.com/user-attachments/assets/47310c72-49f1-4f2b-bd7a-e20c6d8ef6a9)
- In the above picture there are 2  buffers , because to reduce the loading effect

- Testbench for 4 bit 2 stage Flash ADC
![2_stage_flash_adc_test](https://github.com/user-attachments/assets/a306a022-5bdd-44fd-b736-74fc7d760743)

- output of 4 bit 2 stage Flash ADC
- you can see small part with claer resolution 
![2_stage_flash_adc_output1](https://github.com/user-attachments/assets/5a443065-0505-445b-a30a-dc73322746ec)
- full obtained output
![2_satge_flash_adc_output2](https://github.com/user-attachments/assets/f6f80e71-ec47-4a01-a258-e4869d7fe8b4)

# Refrence 
- Short notes by Phillip E.Allen
- https://drive.google.com/drive/folders/1l3RUkgVgxhLF61Y6qqgLO9Xr1yyfzzXa
- Books and Papers
- https://drive.google.com/drive/folders/1Y61bhNi8qomxfmtFd93t7pkEo1Sk2XVQ







  





  

















