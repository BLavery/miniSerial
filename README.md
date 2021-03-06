# miniSerial
Very lean software-based Serial substitute.

### 2019 - This is no longer being maintained by the original author.
### Please feel free to fork, copy, adapt if you find it useable

This library was designed for $3 STM32F030F4P6 ARM M0 board, which is limited to 16k of flash. This "baby" board has difficulty compiling the regular Serial function into your sketches.  MiniSerial has a minimal flash footprint, and uses no interrupts. Its functions are simple, a subset of the "print()" type functions of regular Serial.

<img align="right" src="STM32F030-Dev-Brd.jpg">Baudrate is configurable. 19200 looks ideal, but higher than that is no good. Pins are configurable, and are driven only by digitalWrite and digitalRead.

Receive functions are buffered, and your sketch suffers no blocking. But you MUST supply a Serial.run() call in your loop(), and that must be called at high speed without other code doing any delay() or blocking. (For example, a 50 uSec delay will miss a complete "bit" at 19200.) If your loop() has code than is disturbing serial reception, try progressively lowering the baudrate.

Transmit functions are not buffered. Your loop() code will block during transmit. (Eg about 0.6 mSec/chr at 19200.) But note that while your loop() code will wait for the UART transmit function to complete, the UART receive will still be processing and buffering. 

Serial functions:

	#include "miniSerial.h"      // that's it! You have a "Serial"
	
	void begin(int baudrate = 19200, int txpin = PA9, int rxpin = PA10);  // in setup(), 
	   parameters optional, eg Serial.begin();
	void write(unsigned char data);
	void print(double float_num, int prec=2);	
	void print(char* str);
	void print(int, int = DEC);
	void print(long, int = DEC);
	void println(double float_num, int prec=2);	
	void println(char* str = ""); 
	void println(int, int = DEC);
	void println(long, int = DEC);
	void run(void);  // Serial.run();  needed in loop() to be reading incoming chars (they go to buffer)
	int  read(void); // fetch a char from incoming buffer.   -1 = nothing

Avoid if posible the "double" print function. It consumes a lot of precious flash memory space.

Please find the code here:

https://github.com/BLavery/STM32F030F4P6-Arduino/tree/master/Arduino/libraries/miniSerial

Despite the original target of small STM32 chip, there is no reason that miniSerial may not be quite useable in other scenarios.


V 0.5.0
