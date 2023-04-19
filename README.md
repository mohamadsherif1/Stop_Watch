# Stop_Watch

The main components of the project are:

- An ATmega32 microcontroller with a 1 MHz frequency
- Six common anode 7-segment displays (HDSP5503 or similar)
- A 7447 decoder to convert the binary signals from the microcontroller to the 7-segment signals
- Six NPN transistors (2N2222 or similar) to enable or disable each 7-segment display
- Three push buttons with pull-up or pull-down resistors to trigger the external interrupts
- A 47 uF capacitor, a 1 kΩ resistor and three 100 nF capacitors for power supply filtering
- Two 220 Ω resistors for current limiting

The main logic of the project is as follows:

- The ATmega32 timer1 is configured in CTC mode with a prescaler of 1024 and a compare value of 977, which generates an interrupt every 0.01 second (1/100th of a second).
- The timer1 interrupt service routine increments a global variable that stores the current count value and updates the first four pins of PORTC with the lower four bits of the count value.
- The main loop of the program uses a multiplexing technique to display the count value on the six 7-segment displays. It cycles through each display by enabling its corresponding transistor and sending the appropriate signals through the 7447 decoder. It also turns on or off the decimal point depending on the position of the display.
- The external interrupts INT0, INT1 and INT2 are configured with falling edge, rising edge and falling edge triggers respectively. They are connected to three push buttons that control the stop watch functionality.
- The INT0 interrupt service routine resets the count value to zero and clears the timer1 register.
- The INT1 interrupt service routine pauses the timer1 by disabling its interrupt.
- The INT2 interrupt service routine resumes the timer1 by enabling its interrupt.

The code for the project is written in C language and can be compiled using any AVR compiler. The code is given below:
