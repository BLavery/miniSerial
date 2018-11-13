# miniSerial
Very lean software-based Serial substitute.

This library was designed for STM32F030F4P6 ARM M0 board, which is limited to 16k of flash, and has difficulty fitting in the regular Serial function in your sketches.  MiniSerial has a minimal flash footprint, and uses no interrupts. Its functions are simple, and do NOT align with the "println()" type functions of regular Serial, because the print functionality is code-expensive.

Baudrate is configurable. 19200 looks ideal. Pins are configurable, and are driven only by digitalWrite and digitalRead.

Receive functions are buffered, and your sketch suffers no blocking. But you MUST supply a Serial.run() call in your loop(), and that must be called at high speed without other code doing any delay() or blocking.

Transmit functions are not buffered. Your loop() code will block during transmit. (Eg about 0.6 mSec/chr at 19200.) But note that while your code will wait for the transmit function to complete, the UART receive will still be processing. 



Please find the code here:

https://github.com/BLavery/STM32F030F4P6-Arduino/tree/master/Arduino/libraries/miniSerial

Despite the original target of small STM32 chip, there is no reason that miniSerial cannot be used in other scenarios.
