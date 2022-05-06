# PLL 
 A phase-locked loop or PLL is a control system that generates an output signal whose phase is related to the phase of an input signal. \
 PLLs are widely used for synchronization purposes, including clock generation and distribution inside the SoC’s.
 We will be building the PLL using 28nm
 technology node.
 
 
 <h2> Contents: </h2>

1. [28/32nm PDK](#28/32nm-PDK)
2. [Tools Overview](#Tool-Overview)
3. [PLL introduction](#PLL-introduction)
4. [Circuit Details](#Circuit-Details)
5. [Circuit Design](#Circuit-Design)  
    - [Charge pump(CP)](#Charge-pump(CP))
    - [Phase Frequency Detector(PFD)](#Phase-Frequency-Detector(PFD))
    - [Low Pass Filter(LPF)](#Low-Pass-Filter(LPF))
    - [Voltage Controlled Oscillator(VCO)](#Voltage-Controlled-Oscillator(VCO))
    - [Frequency Divider(FD)](#Frequency-Divider(FD))
6. [Simulations](#Simulations)
7. [References](#References)
8. [Acknowlegements](#Acknowlegements)

 
 
 
 ### 28/32nm PDK
  32-nanometer refers to the average half-pitch (i.e., half the distance between identical features) of a memory cell at this technology level.  The 28-nanometer node was an intermediate half-node die shrink based on the 32-nanometer process.
  
  So for the design of the PLL we will be using the 28/32nm PDK file.


### Tools Overview 

***Synopsys Custom Compiler Tool Details***

The [Synopsys Custom Compiler™](https://www.synopsys.com/implementation-and-signoff/custom-design-platform/custom-compiler.html) design environment is a modern solution for full-custom analog, custom digital, and mixed-signal IC design. As the heart of the Synopsys Custom Design Platform, Custom Compiler provides design entry, simulation management and analysis, and custom layout editing features. It delivers industry-leading productivity, performance, and ease-of-use while remaining easy to adopt for users of legacy tools.
 
 ![custom_compiler](https://github.com/bharath19-gs/6T_SRAM_CELL/blob/main/6T_SRAM/custom_compiler.png)
 
 - PrimeWave Design Environment
 PrimeWave Design Environment is a comprehensive and flexible environment for simulation setup and analysis of analog, RF, mixed-signal design, custom-digital and memory designs within the Synopsys Custom Design Platform.

- PrimeSim HSPICE
 PrimeSim HSPICE is the accurate circuit simulator and offers foundries-certified MOS device models with state-of-theart simulation and analysis algorithms. It is used for building digital MOSFET circuits using 28nm technology.
 
 

<h2> PLL introduction <h2>

 ### What does a PLL(Phase-locked loop) contain?
  
 Phase locked loops mainly consist of the following 4 components 
  - Charge pump(CP)
  - Phase Frequency Detector(PFD)
  - Voltage Controlled Oscillator(VCO)
  - Low Pass Filter(LPF) 
  - Frequency Divider(FD)
 
 
  A phase-locked loop or PLL is a closed loop feedback circuit comprises of four main blocks phase frequency detector (PFD), charge pump (CP), low pass filter (LPF) and voltage-controlled oscillator (VCO) PLL as shown in Fig.1. These blocks are connected to form a closed loop feedback network so as to synchronize the output with the input in both phase and frequency. And this loop continues to run until PLL locked condition is achieved i.e., either zero or constant phase difference between the reference input and the feedback pulse from the output of PLL. PLL is castoff as on chip clock generator, frequency synthesizer and clock and data recovery system in radio, computers and telecommunication system. In general, as technology scale down a PLL with wide tuning range, low jitter, and PLL operating at high frequencies are preferred.
  
  ![img](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/PLL.png)
  
### Circuit Specifications

The specifications for PLL to be designed are:

Corner - 'TT' (Typical-Typical/Normal-Normal)\n
Supply Voltage - 1.5V<br />
Room Temperature - 27<br />
VCO mode and PLL mode<br />
Input Fmin=5Mhz; Fmax=12.5Mhz<br />
Multiplier - 8x<br />
Jitter(RMS) < ~20ns<br />
Duty Cycle - 50%<br />
 
![pll](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/PLL_final.png)

The above image shows the basic PLL design with all the internal blocks integrated.

### Circuit Design 
 Let us discuss about each block in the PLL circuit design.

  1. Phase Frequency Detector(PFD)

 The phase frequency detector(PFD) is responsible for comparing 2 signals(the reference signal and the output signal).So, from the comparing of the 2 signals we get to know that which signal is leading/lagging comnmpared to the other,The ouput of PFD is in digital form.
 
 The referred design used : </br>
 ![PFD](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/PFD.png)
 
 The PFD schematic can be observed below with the symbol generated using the Tool for the Pre-layout simulations.
 ![PFD](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/Phase_detector_schematic.png)
 ![PFD](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/Phase_detector_symbol.png)
 
 2. Charge pump(CP)
 
 The CP converts the digital output from PFD to an analog signal . This analog signal is what would control the Voltage Controlled Oscillator(VCO). The analog ouput from CP is passed through a low pass filter before connecting to the VCO. This low pass filter can help smoothen the signal in addition to stabilizing the feedback loop.
 
  The referred design used : </br>
 ![CP](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/CP.png)
 
 
 The CP schematic can be observed below with the symbol generated using the Tool for the Pre-layout simulations.
![CP](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/Charge_pump_schematic.png)
 ![CP](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/Charge_pump_symbol.png)

 

 3. Low Pass filer(LPF)
 
 A low pass filter is used to remove out the noise from a signal, noise are high frequency signals.
  In the case of our PLL it is used to smoothen out the signal for the Voltage Controlled Oscillator(VCO).
  
 ![LPF](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/Low_pass_filter.png)
 
 4. Voltage Controlled Oscillator(VCO)
 
  Voltage controlled oscillators are the actual parts which produces alternating digital clock signal. The frequency of this clock signal can be controlled by input voltage, hence the name.
  
   The referred design used : </br>
 ![VCO](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/VCO.png)
 
  The PFD schematic can be observed below with the symbol generated using the Tool for the Pre-layout simulations.
 ![VCO](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/VCO_schematic.png)
 ![VCO](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/VCO_symbol.png)

 
 
 5. Frequency Divider(FD)
 
  A PLL with a frequency divider on its feedback loop is called a clock multiplier PLL. Such a PLL can make clock signals which are multiples of the reference signals.
   ![FD](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/Freq_divider_schematic.png)
 ![FD](https://github.com/bharath19-gs/avsdpll28nm/blob/main/pll_images/Freq_divider_symbol.png)



### Simulations




### References 
[1] [PLL Design using 130nm PDK](#https://github.com/lakshmi-sathi/avsdpll_1v8) </br>
[2] [Phase locked loop](#https://github.com/ShubhamTomar9675/Phase_Locked_Loop) </br>



### Acknowlegements

Kunal Ghosh, Co-founder , VSD Corp. Pvt. Ltd. - kunalpghosh@gmail.com </br>
Muthukrishnan Chinnasamy , CEO of SFAL </br>
Montu Makadia, SFAL </br>
Lakshmi S, Instructor - 8x PLL Clock Multiplier IP </br>



