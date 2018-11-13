# miniSerial
Very lean software-based Serial substitute.

This library was designed for $3 STM32F030F4P6 ARM M0 board, which is limited to 16k of flash. This "baby" board has difficulty compiling the regular Serial function into your sketches.  MiniSerial has a minimal flash footprint, and uses no interrupts. Its functions are simple, but they do NOT align with the "println()" type functions of regular Serial.

Baudrate is configurable. 19200 looks ideal. Pins are configurable, and are driven only by digitalWrite and digitalRead.

Receive functions are buffered, and your sketch suffers no blocking. But you MUST supply a Serial.run() call in your loop(), and that must be called at high speed without other code doing any delay() or blocking. (For example, a 50 uSec delay will miss a complete "bit" at 19200.) 

Transmit functions are not buffered. Your loop() code will block during transmit. (Eg about 0.6 mSec/chr at 19200.) But note that while your code will wait for the UART transmit function to complete, the UART receive will still be processing and buffering. 



Please find the code here:

https://github.com/BLavery/STM32F030F4P6-Arduino/tree/master/Arduino/libraries/miniSerial

Despite the original target of small STM32 chip, there is no reason that miniSerial may not be quite useable in other scenarios.
