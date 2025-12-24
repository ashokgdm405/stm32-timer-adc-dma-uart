STM32 Blackpill Bare-Metal ADC-DMA-UART

This repository contains a bare-metal implementation for the STM32 Blackpill development board (STM32F411CEU6 microcontroller) that demonstrates the following functionality:

1.100Hz Timer: A general-purpose timer (TIM2) is configured to generate an update event every 10ms (100Hz).

2.Timer-Triggered ADC: The TIM2 update event is used as an external trigger to start an Analog-to-Digital Conversion (ADC1) on Channel 0 (PA0).

3.DMA Transfer: The ADC conversion result is automatically transferred to a memory buffer using Direct Memory Access (DMA2 Stream 0, Channel 0).

4.UART Transmission: Upon completion of the DMA transfer (which is configured in circular mode), an interrupt is triggered. The Interrupt Service Routine (ISR) formats the ADC result into a human-readable string and initiates a UART transmission via DMA (DMA1 Stream 6, Channel 4) on USART2 (PA2/PA3).

5.Serial Output: The ADC result is continuously sent via UART (115200 baud, 8N1) for display on a serial terminal like PuTTY.

Hardware Configuration

•Microcontroller: STM32F411CEU6 (Blackpill)

•ADC Input: PA0 (Analog Channel 0)

•UART: USART2 (PA2 - TX, PA3 - RX)

•Clock: System Clock configured to 100MHz using HSI and PLL.

Bare-Metal Implementation Details

The code is written entirely by directly manipulating the peripheral registers, without using the STM32 HAL or Cube libraries.

•registers.h: Contains the base addresses, register structure definitions, and bit-field macros for RCC, GPIO, TIM2, ADC1, DMA1, DMA2, and USART2.

•main.c: Contains the main logic, peripheral configuration functions (SystemClock_Config, GPIO_Config, TIM2_Config, ADC1_Config, DMA_Config, USART2_Config), and the DMA Transfer Complete Interrupt Service Routine (DMA2_Stream0_IRQHandler).

•startup.s: A minimal assembly startup file containing the vector table and the Reset_Handler for initializing the stack, copying data, and clearing BSS.

•stm32f411ceux_flash.ld: A linker script defining the memory layout for the STM32F411CEU6.

•Makefile: A simple Makefile to compile the project using the arm-none-eabi-gcc toolchain.

Build Instructions

1.Install Toolchain: Ensure you have the ARM GNU Embedded Toolchain installed.

2.Compile: Navigate to the project directory and run make.

3.Flash: The compiled binary will be located at build/stm32_adc_dma_uart.bin. Use an ST-Link programmer and a tool like st-flash or OpenOCD to flash the binary to the Blackpill board.

 Output (Simulated Demonstration)

Since a physical demonstration is not possible in this environment, the following simulated materials show the expected behavior of the compiled firmware.

Simulated Serial Terminal Output

The output shows the ADC value being printed at a 100Hz rate.

text ADC: 1024 ADC: 1124 ADC: 1224 ADC: 1324 ADC: 1424 ADC: 1524 ADC: 1624 ADC: 1724 ADC: 1824 ADC: 1924 ... (continues at 100Hz)

Simulated Oscilloscope Capture

This image simulates the sampling of a 10Hz sine wave by the 100Hz timer-triggered ADC.

•Blue Line: Simulated Analog Input (Voltage/Value)

•Red Steps: The 12-bit ADC samples (0-4095) taken at 100Hz.

•Green Dashed Lines: The 100Hz Timer Trigger points.


 Author
 
 Gaddam Ashok
