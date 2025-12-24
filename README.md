STM32 Timer Triggered ADC with DMA and UART

 Project Description:

This project implements a real-time data acquisition system on an STM32 Blackpill microcontroller. A hardware timer running at 100 Hz is used to trigger ADC conversions periodically. The ADC conversion results are transferred to memory using DMA (Direct Memory Access) to minimize CPU intervention. Once the DMA transfer is complete, the acquired ADC data is sent to a PC via UART and displayed on a serial terminal such as PuTTY.

The project demonstrates efficient use of STM32 hardware peripherals and highlights the advantages of hardware-triggered, DMA-based designs over software polling methods.

 Objectives:

.Generate a precise 100 Hz timer
.Trigger ADC conversions using timer hardware (TRGO)
.Transfer ADC results using DMA
.Send ADC data over UART
.Display real-time ADC values on a serial terminal
.Avoid software delays and polling

 Hardware Requirements

.STM32 Blackpill (STM32F401 / STM32F411)
.ST-Link V2 (for programming and debugging)
.USB-to-UART converter (CP2102 / CH340 / FTDI) or USB CDC
.Potentiometer (analog input source)
.Breadboard and jumper wires

 Hardware Connections:

.ADC Input (Potentiometer)
.Signal	STM32 Pin
.ADC Input	PA0
.VCC	3.3V
.GND	GND

3.3V ──┐
       ├── POT ─── PA0 (ADC)
GND ───┘

UART Connection:

.STM32 Pin	USB-UART
.PA9 (TX)	RX
.PA10 (RX)	TX
.GND	GND

 System Architecture:
 
Timer (100 Hz)
      ↓
ADC (Hardware Triggered)
      ↓
DMA (Automatic Data Transfer)
      ↓
DMA Transfer Complete Interrupt
      ↓
UART Transmission
      ↓
PC Serial Terminal (PuTTY)

 Software Overview:
 
Peripherals Used

.Timer (TIMx) – Generates a 100 Hz trigger signal
.ADC – Converts analog voltage to digital data
.DMA – Transfers ADC data directly to memory
.UART (USARTx) – Sends data to PC
.Key Design Features
.Hardware-triggered ADC (no software start)
.DMA-based data transfer (no polling)
.Deterministic sampling rate
.Low CPU utilization
.Suitable for real-time embedded systems

 How to Run the Project:

.Connect the hardware as described above
.Flash the firmware using ST-Link
.Open a serial terminal (PuTTY / Tera Term)
.Baud rate: 115200
.Data bits: 8
.Stop bits: 1
.Parity: None
.Rotate the potentiometer
.Observe ADC values updating at 100 Hz

 Sample UART Output:
 
.ADC Value: 1023
.ADC Value: 1108
.ADC Value: 1240
.ADC Value: 1365

 Results

.ADC data is sampled at a fixed 100 Hz rate
.DMA ensures efficient, CPU-independent data transfer
.UART output confirms successful end-to-end data flow


 Comparison:          Software Polling      Hardware Triggering

.Sampling accuracy         Low	               High
.Timing jitter	           Present	          Minimal
.CPU usage                 High	             Low
.Scalability               Limited	           High

 Future Improvements:

.Multi-channel ADC sampling
.Circular DMA buffer
.USB CDC instead of UART
.Data logging to SD card
.Digital signal processing on acquired data

 Author
 Gaddam Ashok
