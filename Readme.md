# PLL 
 A phase-locked loop or PLL is a control system that generates an output signal whose phase is related to the phase of an input signal. \
 PLLs are widely used for synchronization purposes, including clock generation and distribution inside the SoC’s.
 We will be building the PLL using 28nm
 technology node.
 
 
 <h2> Contents: </h2>

1. [28/30nm PDK]
2. [tool used]
3. [PLL introduction]
4. [Circuit details]
5. [Circuit Design]
6. [Simulations]. 
7. [Acknowlegements]
8. [Contact]
 
 
 
### What does a PLL(Phase-locked loop) contain?
  Phase locked loops mainly consist of the following 4 components 
  - Charge pump(CP)
  - Phase Frequency Detector(PFD)
  - Voltage Controlled Oscillator(VCO)

  - Frequency divider
  A phase-locked loop or PLL is a closed loop feedback circuit comprises of four main blocks phase frequency detector (PFD), charge pump (CP), low pass filter (LPF) and voltage-controlled oscillator (VCO) PLL as shown in Fig.1. These blocks are connected to form a closed loop feedback network so as to synchronize the output with the input in both phase and frequency. And this loop continues to run until PLL locked condition is achieved i.e., either zero or constant phase difference between the reference input and the feedback pulse from the output of PLL. PLL is castoff as on chip clock generator, frequency synthesizer and clock and data recovery system in radio, computers and telecommunication system. In general, as technology scale down a PLL with wide tuning range, low jitter, and PLL operating at high frequencies are preferred.
  
  ![img](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/PLL.png)
  
### Circuit Details

The concept behind PFD is it compare the two-input signal and produces error signal proportional to the difference between the input signals so for PLL it is used as error detecting block. PFD uses two D-FF's whose input is kept always at high potential, and the reference signal is provided at the clock input of one the D-FF i.e., CLKREF and output of VCO is feed-back to clock input of another D-FF i.e., CLKFB. An AND gate is provided at the output of both D-FFs to generate a reset signal and set the output of both the D-FFs to zero whenever both the signal QA or UP and QB or DOWN is high.
A charge pump is a bipolar switch that is controlled by the three states of the PFD. Conventional charge pump has two symmetrical current sources and two transistors that acts as switch. It generates both the polarity of current pulses into LPF. LPF is used in PLL to get rid of the high frequency components in the output of the PFD. It also removes the high frequency noise.
VCO is the most important block in PLL. It produces high frequency output signal in phase with reference input signal to PLL. In an ideal VCO, there is a linear relationship between output frequency and control voltage.

--- write about the frequency divider----
![pll](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/PLL_final.png)

The above image shows the basic PLL design with all the components integrated.

### Circuit design 
 Let us discuss about each block in the PLL circuit design.
1. Charge pump (CP)
   





