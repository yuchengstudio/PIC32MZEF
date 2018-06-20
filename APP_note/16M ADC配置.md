#                                                          目录




# 2.0  配置思路
```
object: 16M ADC to sample a 2M signal.

The max throughput is achievable using all the ADC tied to the same input and setting everything up to make sure everything lines up correctly. 
The maximum rate for a single channel is the 5 Msps that you discovered in your description. 

Meaning, he cannot achieve the 16 MSPS ADC sampling rate using just one channel

For reference, here is the theory for getting a higher sample rate:
<<<<<<<<<>>>>>>>>>>>
Consider ADC1, ADC2, ADC3, ADC4 configured to sample and convert pins AN0, AN1, AN3, AN3 respectively. 
The minimum sample time for 12-bit and this mode would be 5TAD. With an ADC clock of 50MHz, TAD=20ns. So 5TAD = 100ns. 

The operation is that AN0 is sampled for 5TAD(100ns) and then converted. At the end of the sampling, AN1 starts sampling and same for AN2 and AN3. By the time AN3 sampling has completed, AN0 conversion has completed and can be sampled again. In this way, the 4 analog inputs are cascaded and all sampling at 100ns (10Msps). 
For 10-bit and 8-bit resolution, the rate can be increased because 4TAD or 3TAD can be used respectively. 


PIC32MZxxEFxx 10msps Example Assumptions: 
• SYSCLK=200mhz 
• PBxCLK=100MHz 
• Analog input signal source connected in parallel to AN0, AN1, AN2 & AN3 

Configure ADC1-4 with: 
o ADCCLK (TAD) = 50Mhz = 20ns 
o Configure ADC1 AN0 ADCTRG1<TRGSRC0> = OCMP1 
o Configure ADC2 AN1 ADCTRG1<TRGSRC0> = OCMP3 (PIC32MZxxEFxx) 
o Configure ADC3 AN2 ADCTRG1<TRGSRC0> = OCMP5 (PIC32MZxxEFxx) 
o Configure ADC4 AN3 ADCTRG1<TRGSRC0> = TIMER3 
o Enable ADCs 

Configure OCMP1,3,5 to use TIMER3 with: 
o OCMP1-3 not connected to any pin through PPS mapping, (i.e. internal only) 
o Configure OCMP1,3,5 in any of the (3) single compare match modes available. 
o Configure OC1R = 5. (i.e. Trigger ADC1_AN0 Conversion) 
o Configure OC3R = 10 (i.e. Trigger ADC2_AN1 Conversion), (PIC32MZxxEFxx) 
o Configure OC5R = 15 (i.e. Trigger ADC3_AN2 Conversion), (PIC32MZxxEFxx) 
o Enable Output Compare modules 

Configure TIMER3 (Assuming100MHz PBCLK) 
o Clock = PBCLK 
o T3CON<TCKPS> = Prescalar equal 2, (i.e. PBCLK/2=50MHz) 
o TMR3 = 0; 
o PR3 = 20 (i.e. Trigger ADC4_AN3 Conversion) 
o Enable Timer3 

```

