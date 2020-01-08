# 开发板配置
## BoardInit
初始化开发板  

	static void BoardInit(void)
	{
		// In case of TI-RTOS vector table is initialize by OS itself
		#ifndef USE_TIRTOS
		    // Set vector table base
			#if defined(ccs) || defined(gcc)
		    	MAP_IntVTableBaseSet((unsigned long)&g_pfnVectors[0]);
			#endif
			#if defined(ewarm)
		    	MAP_IntVTableBaseSet((unsigned long)&__vector_table);
			#endif
		#endif //USE_TIRTOS
	
	    // Enable Processor
	    MAP_IntMasterEnable();
	    MAP_IntEnable(FAULT_SYSTICK);
	
	    PRCMCC3200MCUInit();
	}

### Outline
[`IntVTableBaseSet`](#func) 设置中断向量表基地址  
[`IntMasterEnable`](#func) 允许处理器中断  
[`IntEnable`](#func) 允许中断  
[`PRCMCC3200MCUInit`](#func) 初始化MCU  

### 功能函数  
#### <span id="func">IntVTableBaseSet</span>
> Sets the NVIC VTable base. This function is used to specify a new base address for the VTable. This function must be called before using IntRegister() for registering any interrupt handler.  

	void IntVTableBaseSet(unsigned long  ulVtableBase) 
`ulVtableBase`：中断向量表基地址。  

#### <span id="func">IntMasterEnable</span>
> Enables the processor interrupt. Allows the processor to respond to interrupts. This does not affect the set of interrupts enabled in the interrupt controller; it just gates the single interrupt from the controller to the processor.

	tBoolean IntMasterEnable(void)  


#### <span id="func">IntEnable</span>
> Enables an interrupt. The specified interrupt is enabled in the interrupt controller. Other enables for the interrupt (such as at the peripheral level) are unaffected by this function.

	void IntEnable(unsigned long  ulInterrupt)  
`ulInterrupt`：需要使能的中断号。`FAULT_SYSTICK`是SysTick的中断号常量，中断号是15，在`hw_ints.h`中定义。  

#### <span id="func">PRCMCC3200MCUInit</span>  
> MCU Initialization Routine. This function sets mandatory configurations for the MCU.  

	void PRCMCC3200MCUInit(void)

加电启动或从低功耗休眠模式退出时，应用程序应该通过调用`PRCMCC3200MCUInit()`配置MCU参数。  


## PinMuxConfig  
引脚复用配置  

	void PinMuxConfig(void)
	{
	    // Enable Peripheral Clocks 
	    MAP_PRCMPeripheralClkEnable(PRCM_GPIOA1, PRCM_RUN_MODE_CLK);
	    MAP_PRCMPeripheralClkEnable(PRCM_UARTA0, PRCM_RUN_MODE_CLK);
	
	    // Configure PIN_55 for UART0 UART0_TX
	    MAP_PinTypeUART(PIN_55, PIN_MODE_3);
	
	    // Configure PIN_57 for UART0 UART0_RX
	    MAP_PinTypeUART(PIN_57, PIN_MODE_3);
	
	    // Configure PIN_64 for GPIOOutput
	    MAP_PinTypeGPIO(PIN_64, PIN_MODE_0, false);
	    MAP_GPIODirModeSet(GPIOA1_BASE, 0x2, GPIO_DIR_MODE_OUT);
	
	    // Configure PIN_01 for GPIOOutput
	    MAP_PinTypeGPIO(PIN_01, PIN_MODE_0, false);
	    MAP_GPIODirModeSet(GPIOA1_BASE, 0x4, GPIO_DIR_MODE_OUT);
	
	    // Configure PIN_02 for GPIOOutput
	    MAP_PinTypeGPIO(PIN_02, PIN_MODE_0, false);
	    MAP_GPIODirModeSet(GPIOA1_BASE, 0x8, GPIO_DIR_MODE_OUT);
	}

### Outline
[`PRCMPeripheralClkEnable`](#func1) 允许外设时钟  
[`PinModeSet`](#func2)  配置GPIO引脚，为指定引脚复用配置模式   
[`PinConfigSet`](#func3) 配置引脚输出驱动强度和类型
[`GPIODirModeSet`](#func)  

### 功能函数  

#### <span id="func1">PRCMPeripheralClkEnable</span>
> Enable clock(s) to peripheral.

	void PRCMPeripheralClkEnable(
		unsigned long  ulPeripheral,
		unsigned long  ulClkFlags)


`ulPeripheral`：需要使能外设的外设号，在`prcm.h`中定义。常见的如`PRCM_GPIOAx`,`PRCM_UARTAx`  
`ulClkFlags`：时钟标志。`PRCM_RUN_MODE_CLK`表示运行模式时钟，`PRCM_SLP_MODE_CLK`表示睡眠模式时钟。   

#### <span id="func2">PinModeSet</span>
> Configures pin mux for the specified pin.

	void PinModeSet(
		unsigned long  ulPin,
		unsigned long  ulPinMode)

`ulPin`：引脚号，*PIN_01~64*，在`pin.h`中定义。  
`ulPinMode`：引脚模式，需要查外设引脚分配表。    

#### <span id="func3">PinConfigSet</span>
> Configure Pin output drive strength and Type

	void PinConfigSet(
		unsigned long  ulPin, 
		unsigned long  ulPinStrength,
		unsigned long  ulPinType)

`ulPin`：引脚号，*PIN_01~64*，在`pin.h`中定义。  
`ulPinStrength`：引脚强度，配置输出驱动电流(2mA, 4mA, 6mA)分别对应`PIN_STRENGTH_2MA`,`PIN_STRENGTH_4MA` ,`PIN_STRENGTH_6MA`   
`ulPinType`：引脚类型，一般设置为`PIN_TYPE_STD`标准输入输出

#### <span id="func3">GPIODirModeSet </span>
> Sets the direction and mode of the specified pin(s). This function will set the specified pin(s) on the selected GPIO port as either an input or output under software control, or it will set the pin to be under hardware control.  The pin(s) are specified using a bit-packed byte, where each bit that is set identifies the pin to be accessed, and where bit 0 of the byte represents GPIO port pin 0, bit 1 represents GPIO port pin 1, and so on.


	void GPIODirModeSet(unsigned long  ulPort,
		unsigned char  ucPins,  
		unsigned long  ulPinIO)

`ulPort`：GPIO端口基地址，在`hw_memmap.h`中定义。  
`ucPins`：引脚位权，4个GPIO组中8个GPIO的引脚位权从低到高依次为0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80。即一个GPIO组有8个Pin，用一个字节表示，1个Pin对应1个bit。    
`ulPinIO`：GPIO引脚方向，枚举类型：`GPIO_DIR_MODE_IN`,`GPIO_DIR_MODE_OUT`。


