/**
  @page ADC_TriggerMode ADC3 conversion using Trigger Mode

  @verbatim
  ******************** (C) COPYRIGHT 2016 STMicroelectronics *******************
  * @file    ADC/ADC_TriggerMode/readme.txt 
  * @author  MCD Application Team
  * @brief   Description of the ADC Trigger Mode example.
  ******************************************************************************
  * @attention
  *
  * <h2><center>&copy; Copyright (c) 2016 STMicroelectronics.
  * All rights reserved.</center></h2>
  *
  * This software component is licensed by ST under BSD 3-Clause license,
  * the "License"; You may not use this file except in compliance with the
  * License. You may obtain a copy of the License at:
  *                        opensource.org/licenses/BSD-3-Clause
  *
  ******************************************************************************
  @endverbatim

@par Example Description 

How to use ADC and TIM2 to continuously convert data from an ADC channel. 
Each time an external trigger is generated by TIM2 a new conversion is started 
by the ADC.

At the end of conversion, an interrupt is generated and the converted data of 
ADC1 DR register is affected to the uhADCxConvertedValue variable in the ADC 
conversion complete call back function (HAL_ADC_ConvCpltCallback).

The timer is used to trigger an ADC measure at 20 KHz.

Configuration of the timer to trig an ADC measure at 20 Khz:
  From the reference manual, Reset and Clock control part, Timer 2 is clocked on PCLK1.
  The function SystemClock_Config() configures the clock divider as follows:
  1) The system clock is 72 MHz.
  2) AHB  Prescaler = 1 => AHB clock is 72 MHz.
  3) APB1 Prescaler = 2 => PCLK1 clock is 36 MHz.
  4) For Timer 2, as APB1 Prescaler = 2, Timer 2 Clock is PCLK1 clock X 2 = 72 Mhz.

  For a 20 Khz frequency, we need 72 MHz / 20 KHz = 3600 clock cycle.
  So, in TIM_Config function, we set the following period: htim.Init.Period = 3600;

The voltage on pin PC.01 (ADC_CHANNEL_7)can vary using the board potentiometer RV2.

Remark: LED3 is ON when there is an error in initialization.

@par Directory contents 

  - ADC/ADC_TriggerMode/Inc/stm32f3xx_hal_conf.h    HAL configuration file
  - ADC/ADC_TriggerMode/Inc/stm32f3xx_it.h          DMA interrupt handlers header file
  - ADC/ADC_TriggerMode/Inc/main.h                  Header for main.c module  
  - ADC/ADC_TriggerMode/Src/stm32f3xx_it.c          DMA interrupt handlers
  - ADC/ADC_TriggerMode/Src/main.c                  Main program
  - ADC/ADC_TriggerMode/Src/stm32f3xx_hal_msp.c     HAL MSP file 
  - ADC/ADC_TriggerMode/Src/system_stm32f3xx.c      STM32F3xx system source file

@par Hardware and Software environment 

  - This example runs on STM32F303xC devices.

  - This example has been tested with STM32303C-EVAL RevC board and can be
    easily tailored to any other supported device and development board.

@par How to use it ? 

In order to make the program work, you must do the following :
 - Open your preferred toolchain 
 - Rebuild all files and load your image into target memory
 - Run the example

 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */
