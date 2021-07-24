# Two stage operational amplifier design:

# --->WORKING WITH ESIM ,NGSPICE AND SKY130 MODELS

1. Go to esim click on new project ,give name file will be saved then click on open schematic window

2. Using place component ,place all necessary components for the circuit on to the schematic window.

3. Connecte all components using wires & annotate all the components using annotate option.

4. To verify errors in circuit electrical rules check option will help

5. Then generate netlist will generate spice file which will helful for ngspice circuit simulation.

6. In generated spice file add sky130 models by using its library which is available in sky130 folder and edit netlist accordingly,the generated netlist is of type .cir

7. Run the .cir file to get plots. 


# Circuit Diagram on eSim:
![circuit](https://user-images.githubusercontent.com/86840635/126867285-ff1e1ed9-6a95-44b9-a4b7-df7b59e1f46c.PNG)

# Code for AC Analysis:

* C:\Users\Rohini\eSim-Workspace\Op-Amp\Op-Amp.cir

.lib "sky130_fd_pr/models/sky130.lib.spice" tt

xM1  Net-_M1-Pad1_ vin1 Net-_M1-Pad3_ GND sky130_fd_pr__nfet_01v8 w=1.05 l=0.35		
xM2  Net-_C1-Pad2_ vin2 Net-_M1-Pad3_ GND sky130_fd_pr__nfet_01v8 w=1.05 l=0.35		
xM3  vdd Net-_M1-Pad1_ Net-_M1-Pad1_ vdd sky130_fd_pr__pfet_01v8 w=0.7 l=0.35
xM4  vdd Net-_M1-Pad1_ Net-_C1-Pad2_ vdd sky130_fd_pr__pfet_01v8 w=0.7 l=0.35		
xM5  Net-_M1-Pad3_ vbias GND GND sky130_fd_pr__nfet_01v8 w=4.9 l=0.35
xM6  vdd Net-_C1-Pad2_ vout vdd sky130_fd_pr__pfet_01v8 w=19.6 l=0.35
xM7  vout vbias GND GND sky130_fd_pr__nfet_01v8 w=13.75 l=0.35		
xM8  vbias vbias GND GND sky130_fd_pr__nfet_01v8 w=3.5 l=0.35	
C1  vout Net-_C1-Pad2_ 800f	
C2  vout GND 2p		
I1 vdd vbias 20u
Vdd vdd  GND 1.8

V1 vin1 vin2 ac 20 0
V2 vin2 GND 0.84

.ac dec 20 1Hz 1Meg
.control
run
plot  db(vin1)  
plot db(vout)
.endc

.end

# Gain Waveforms:

![gain](https://user-images.githubusercontent.com/86840635/126867328-99e768b8-e25d-45d1-ad4b-d419bc712b85.PNG)




# Code for DC Analysis:

* C:\Users\Rohini\eSim-Workspace\Op-Amp\Op-Amp.cir

.lib "sky130_fd_pr/models/sky130.lib.spice" tt
		
xM1  Net-_M1-Pad1_ vin1 Net-_M1-Pad3_ GND sky130_fd_pr__nfet_01v8 w=1.05 l=0.35		
xM2  Net-_C1-Pad2_ vin2 Net-_M1-Pad3_ GND sky130_fd_pr__nfet_01v8 w=1.05 l=0.35		
xM3  vdd Net-_M1-Pad1_ Net-_M1-Pad1_ vdd sky130_fd_pr__pfet_01v8 w=0.7 l=0.35
xM4  vdd Net-_M1-Pad1_ Net-_C1-Pad2_ vdd sky130_fd_pr__pfet_01v8 w=0.7 l=0.35		
xM5  Net-_M1-Pad3_ vbias GND GND sky130_fd_pr__nfet_01v8 w=4.9 l=0.35
xM6  vdd Net-_C1-Pad2_ vout vdd sky130_fd_pr__pfet_01v8 w=19.6 l=0.35
xM7  vout vbias GND GND sky130_fd_pr__nfet_01v8 w=13.75 l=0.35		
xM8  vbias vbias GND GND sky130_fd_pr__nfet_01v8 w=3.5 l=0.35	
C1  vout Net-_C1-Pad2_ 1p	
C2  vout GND 2p		
I1 vdd vbias 20u
Vdd vdd  GND 1.8

V1 vin1 GND 1v
V2 vin2 GND 1v
.dc V1 0 1.8 0.01

.control

run

plot V(vin1)  
plot V(vout)

.endc

.end
		
# DC Waveform:

![DC](https://user-images.githubusercontent.com/86840635/126867326-b484fd2f-b8f3-4573-b2b0-cd78f5bc590e.PNG)

# Code for Transient Analysis:

* C:\Users\Rohini\eSim-Workspace\Op-Amp\Op-Amp.cir

.lib "sky130_fd_pr/models/sky130.lib.spice" tt
		
xM1  Net-_M1-Pad1_ vin1 Net-_M1-Pad3_ GND sky130_fd_pr__nfet_01v8 w=1.05 l=0.35		
xM2  Net-_C1-Pad2_ vin2 Net-_M1-Pad3_ GND sky130_fd_pr__nfet_01v8 w=1.05 l=0.35		
xM3  vdd Net-_M1-Pad1_ Net-_M1-Pad1_ vdd sky130_fd_pr__pfet_01v8 w=0.7 l=0.35
xM4  vdd Net-_M1-Pad1_ Net-_C1-Pad2_ vdd sky130_fd_pr__pfet_01v8 w=0.7 l=0.35		
xM5  Net-_M1-Pad3_ vbias GND GND sky130_fd_pr__nfet_01v8 w=4.9 l=0.35
xM6  vdd Net-_C1-Pad2_ vout vdd sky130_fd_pr__pfet_01v8 w=19.6 l=0.35
xM7  vout vbias GND GND sky130_fd_pr__nfet_01v8 w=13.75 l=0.35		
xM8  vbias vbias GND GND sky130_fd_pr__nfet_01v8 w=3.5 l=0.35	
C1  vout Net-_C1-Pad2_ 1p	
C2  vout GND 2p		
I1 vdd vbias 20u
Vdd vdd  GND 1.8
		
V1 vin1 GND sine(0.82 1u 1kHz)
V2 vin2 GND 0.82

.tran 0.1m 10m 0m

.control

run

plot V(vin1)  
plot V(vout)

.endc

.end

# Tansient Analysis Output Waveform:

![AC](https://user-images.githubusercontent.com/86840635/126867320-0cbe0acf-5446-41d0-a640-1f2c82c5ad53.PNG)



# Waveforms after eSim simulation: 
![waveform](https://user-images.githubusercontent.com/86840635/126867256-44016f22-434f-4332-a311-b2edda9e04db.jpeg)


# --->TASK PERFORMANCE

1. Introduction to stages of esim marathon 

2. Followed VSD circuit simulation & DAC IP course provided by faculty

3. Joined slack and took help from peers and sirs

4. Researched about ngspice commands and Esim environment.

5. Analysed my circuit using reference circuit in research papers.

6. Debuged my circuit to get needed result

7. Intense process, detailed observation











