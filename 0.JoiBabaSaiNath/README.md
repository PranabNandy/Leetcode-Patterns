# 0.JoibabaSaiNath
## Hash Table Implmentation

![Untitled](https://github.com/user-attachments/assets/ea77d09f-8a87-4e3a-a303-71520f4f4b06)
```c++
	vector<int> v1={1,2,3};
	vector<int> v2={10,20,30,40,50};
	v2=v1; // v2={1,2,3,40,50}  --> In both cases v2.size()==3
	v2=move(v1); //v2={1,2,3,0,0};
```
 
## Similar sources

1. [TheEmbeddedNewTestament](https://github.com/theEmbeddedGeorge/theEmbeddedNewTestament.github.io/tree/master)
2. [AwesomeEmbedded](https://github.com/nhivp/Awesome-Embedded)
3. [Awesome-C](https://github.com/uhub/awesome-c)
4. [Awesome Embedded Systems](https://github.com/embedded-boston/awesome-embedded-systems)


1.https://rmbconsulting.us/publications/a-c-test-the-0x10-best-questions-for-would-be-embedded-programmers/


-------------------------------------------------------------------------------
   
**1) Which endianness is: A) x86 families. B) ARM families. C) internet protocols. D) other processors? One of these is kind of a trick question.**

**2) Explain how interrupts work. What are some things that you should never do in an interrupt function?**

**3) Explain when you should use "volatile" in C.**

**4) Explain UART, SPI, I2C buses. Describe some of the signals in each. At a high-level describe each. Have you ever used any? Where? How? What type of test equipment would you want to use to debug these types of buses? Have you ever used test equipment to do it? Which?**

**5) Explain how DMA works. What are some of the issues that you need to worry about when using DMA?**

**6) Where does the interrupt table reside in the memory map for various processor families?**

**7) In which direction does the stack grow in various processor families?**

8) Implement a Count Leading Zero (CLZ) bit algorithm, but don't use the assembler instruction. What optimizations to make it faster? What are some uses of CLZ?

9) What is RISC-V? What is it's claimed pros or cons?

10) List some ARM cores. For embedded use, which cores were most commonly used in the past? now?

11) Explain processor pipelines, and the pro/cons of shorter or longer pipelines.

12) Explain fixed-point math. How do you convert a number into a fixed-point, and back again? Have you ever written any C functions or algorithms that used fixed-point math? Why did you?

**13) What is a pull-up or pull-down resistor? When might you need to use them?**

14) What is "zero copy" or "zero buffer" concept?

**15) How do you determine if a memory address is aligned on a 4 byte boundary in C?**

`16) What hardware debugging protocols are used to communicate with ARM microcontrollers?`

17) What processor architecture was the original Arduino based on?

**18) What are the basic concepts of what happens before main() is called in C?**

**19) What are the basic concepts of how printf() works? List and describe some of the special format characters? Show some simple C coding examples.**

20) Describe each of the following? SRAM, Pseudo-SRAM, DRAM, ROM, PROM, EPROM, EEPROM, MRAM, FRAM, ...

**21) Show how to declare a pointer to constant data in C. Show how to declare a function pointer in C.**

`22) How do you multiply without using multiply or divide instructions for a multiplier constant of 10, 31, 132?`

**23) When do you use memmove() instead of memcpy() in C? Describe why.**

`24) Why is strlen() sometimes not considered "safe" in C? How to make it safer? What is the newer safer function name?`

**25) When is the best time to malloc() large blocks of memory in embedded processors? Describe alternate approach if malloc() isn't available or desired to not use it, and describe some things you will need to do to ensure it safely works.**

26) Describe symbols on a schematic? What is a printed circuit board?

27) Do you know how to use a logic probe? multimeter? oscilloscope? logic analyzer? function generator? spectrum analyzer? other test equipment? Describe when you might want to use each of these. Have you hooked up and used any of these?

28) What processors or microcontrollers are considered 4-bit? 8-bit? 16-bit? 24-bit? 32-bit? Which have you used in each size group? Which is your favorite or hate?

29) What is ohm's law?

30) What is Nyquist frequency (rate)? When is this important?

31) What is "wait state"?

32) What are some common logic voltages?

33) What are some common logic famlies?

34) What is a CPLD? an FPGA? Describe why they might be used in an embedded system?

35) List some types of connectors found on test equipment.

36) What is AC? What is DC? Describe the voltage in the wall outlet? Describe the voltage in USB 1.x and 2.x cables?

37) What is RS232? RS432? RS485? MIDI? What do these have in common?

38) What is ESD? Describe the purpose of "pink" ESD bags? black or silvery ESD bag? How do you properly use a ground strap? When should you use a ground strap? How critical is it to use ESD protections? How do you safely move ESD-sensitive boards between different parts of a building?

39) What is "Lockout-Tagout"?

40) What is ISO9001? What is a simple summary of it's concepts?

41) What is A/D? D/A? OpAmp? Comparator Other Components Here? Describe each. What/when might each be used?

42) What host O/S have you used? List experience from most to least used.

43) What embedded RTOS have you used? Have you ever written your own from scratch?

44) Have you ever implemented from scratch any functions from the C Standard Library (that ships with most compilers)? Created your own because functions in C library didn't support something you needed?

45) Have you ever used any encryption algorithms? Did you write your own from scratch or use a library (which one)? Describe which type of algorithms you used and in what situations you used them?

45) What is a CRC algorithm? Why would you use it? What are some CRC algorithms? What issues do you need to worry about when using CRC algorithms that might cause problems? Have you ever written a CRC algorithm from scratch?

46) Do you know how to solder? Have you ever soldered surface mount devices?

47) How do you permanently archive source code? project? what should be archived? what should be documented? have you ever written any procedures of how to archive or build a project? How about describing how to install software tools and configuring them from scratch on a brand new computer that was pulled out of a box?

**48) What issues are a concern for algorithms that read/write data to DRAM instead of SRAM?**

49) What is the "escape sequence" for "Hayes Command Set"? Where was this used in the past? Where is it used today?

50) What is the "escape character" for "Epson ESC/P"? Where is this used?

**51) After powerup, have you ever initialized a character display using C code? From scratch or library calls?**

52) Have you ever written a RAM test from scratch? What are some issues you need to test?

**53) Have you ever written code to initialize (configure) low-power self-refreshing DRAM memory after power up (independent of BIOS or other code that did it for the system)? It's likely that most people have never done this.**

**54) Write code in C to "round up" any number to the next "power of 2", unless the number is already a power of 2. For example, 5 rounds up to 8, 42 rounds up to 64, 128 rounds to 128. When is this algorithm useful?**

55) What are two of the hardware protocols used to communicate with SD cards? Which will most likely work with more microcontrollers?

56) What issues concerns software when you WRITE a value to EEPROM memory? FLASH memory?

57) What is NOR-Flash and NAND-Flash memory? Are there any unique software concerns for either?

**58) Conceptually, what do you need to do after reconfiguring a digital PLL? What if the digital PLL sources the clock for your microcontroller (and other concerns)?**

59) What topics or categories of jokes shouldn't you discuss, tell, forward at work?

60) Have you ever used any power tools for woodworking or metalworking?

61) What is a common expression said when cutting anything to a specific length? (old expression for woodworking)

62) Have you ever 3D printed anything? Have you ever created a 3D model for anything? List one or more 3D file extensions.

63) Do you know how to wire an AC wall outlet or ceiling light? Have you ever done either?

64) Have you ever installed a new hard drive / RAM / CPU in a desktop computer?

65) Have you ever installed Windows or Linux from scratch on a computer that has a brand-new hard drive?

66) Have you ever "burned" a CD-R or DVD-R disc? Have you ever created an ISO image of a CD or DVD or USB drive or hard drive?

67) Have you ever read the contents of a serial-EEPROM chip from a dead system (though EEPROM chip is ok)?

68) Have you ever written data to a serial-EEPROM chip before it is soldered down to a PCB?

69) How do you erase an "old school" EPROM chip? (has a glass window on top of the chip)

70) Describe any infrared protocols, either for data or remote controlling a TV.

71) What is the most common protocol is used to communicate with a "smart card"? Have you ever written any software to communicate with a "smart card" in an embedded product?

72) What is I2S? Where is it used? Why might you want to use I2S in an embedded system? Have you ever used it?

73) What is CAN, LIN, FlexRay? Where are they used? Have you ever used any?

74) What is ARINC 429? Where is it commonly used? Have you ever used it?

75) What in-circuit debuggers or programmers have you used? Which one do you like or hate?

76) Do you know any assembler code? For which processor? What assembler code is your favorite or hate? Have you ever written an assembler from scratch?

77) What is "duff's device"? Have you ever used it?

78) What is dual-port RAM? Why would it be useful in some embedded systems? What concerns do you need to worry about when using it? Have you ever used it? How?

79) Have you ever soldered any electronic kits? Have you ever designed your own PCB(s)? Describe. What is a Gerber file?

**80) If you create a circular buffer, what size of buffer might optimized code be slightly faster to execute? why?**

**81) Describe how to multiply two 256-bit numbers using any 32-bit processor without FPU or special instructions. Two or more methods?**


===============================================================================================================================

Some questions for larger embedded systems might also be a good idea:

101. What is a DSP?

102. What are virtual and physical addresses? What is a MMU?

103.Describe different types of Cache. When do you need to flush the cache, when to invalidate cache?

104.What is SIMD?

105.What is a Mailbox register?

106.What is a Cacheline?

107.What is a Mutex?

108.What is Scatter-Gather DMA? What is Ping-Pong DMA?

109.What is WCET and where does it matter?

110.What is Lockstep execution?

===================================================================================



1. what embedded systems experience do you have  
2. Difference between Microcontroller and Microprocessor  
3. Address bus / Data bus  
4. What is clock in controller ? Types of clocks in controller.  
5. What is Embedded system  
6. Types of memory and difference between them  
7. Difference between OS and RTOS  
8. Basic protocols understanding, pins, difference, limitations and how they works : UART, SPI, I2C,
9. UART 
   9.1. UART protocol understanding. How data being transferred using UART. ?  
   9.2. what is baudrate? Difference between bitrate and baudrate? On which baudrate you have used UART ?
   9.3. What maximum baudrate supported for UART.
   9.4. Ever heard of USART. What is it ?
10. I2C 
   10.1. How to read/write data between I2C bus  
   10.2. Does it supports multi-master ? How ? 
11. SPI 
   11.1. Does it supports multi-master ? >A> NO: 
	11.1.1. why it is not supporting ? 
   11.2. How to xfer data between multiple slave/master using SPI  
   11.3. Is there any acknowledgement received for data that we sent using SPI ? Is there in I2C ? 
12. What is DMA ?  
13. What is interrupt ? How to use it ?  
14. What is ISR ?
    14.1. Is it okay to use sleep in ISR ?
    14.2. Can we pass parameters/return type in ISR ?
    14.3. Can we use any function in ISR ?  
15. What happened when interrupt occurs ?  
16. Interrupt latency and turnover time  
17. Timers in Microcontroller. How to generate 1sec. of timer ?  
18. Watchdog timer. Use of it.  
19. What is IoT ?  
20. What is a segmentation fault ? What are the reasons of occurrence of the same ?  
21. Types of Endianness. Difference between them. How to check Endianness using C program. 
22. What is Flash memory ? NAND flash vs NOR flash difference.  
23. Difference bet Asynchronous and Synchronous communication
    >A>
    - No common clk in Async, In sync shared clk
    - Async send 1 byte at a time, sync sends data in form of blocks/frames 
    - Async slower compared to sync 
    - Async can communicate longer distance  
    - Async use start/stop bit for data sync 
    - Async: RS232, RS485   Sync: I2C, SPI
   

  ======================================================================================

  


