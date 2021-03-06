# Lab 8: FRANCISCO ABELARDO GARCÍA AVILÉS

Link to this file in my GitHub repository:

https://github.com/franciscogrca/Digital-electronics-2/edit/main/Lab08-i2c.md

### Arduino Uno pinout

1. In the picture of the Arduino Uno board, mark the pins that can be used for the following functions:

![leyenda](https://user-images.githubusercontent.com/91128800/141957875-8877f8e7-27a4-46f2-a385-461a9cbeca40.png)

![placa](https://user-images.githubusercontent.com/91128800/141957889-ac1f8d2a-ae0e-4bb0-92ce-f5d543c391af.png)


### I2C

1. Code listing of Timer1 overflow interrupt service routine for scanning I2C devices and rendering a clear table on the UART. Always use syntax highlighting and meaningful comments:

```c
/**********************************************************************
 * Function: Timer/Counter1 overflow interrupt
 * Purpose:  Update Finite State Machine and test I2C slave addresses 
 *           between 8 and 119.
 **********************************************************************/
ISR(TIMER1_OVF_vect)
{
    static state_t state = STATE_IDLE;  // Current state of the FSM
    static uint8_t addr = 7;            // I2C slave address
    uint8_t result = 1;                 // ACK result from the bus
    char uart_string[2] = "00"; // String for converting numbers by itoa()

    // FSM
    switch (state)
    {
    // Increment I2C slave address
    case STATE_IDLE:
        addr++;
		if (addr > 7 && addr < 120)
			state = STATE_SEND;
			
		if (addr > 120){
			uart_puts_P("\r\nScan I2C-bus for devices:\r\n");
			addr=0;
		}
		
        // If slave address is between 8 and 119 then move to SEND state

        break;
    
    // Transmit I2C slave address and get result
    case STATE_SEND:
        // I2C address frame:
        // +------------------------+------------+
        // |      from Master       | from Slave |
        // +------------------------+------------+
        // | 7  6  5  4  3  2  1  0 |     ACK    |
        // |a6 a5 a4 a3 a2 a1 a0 R/W|   result   |
        // +------------------------+------------+
        result = twi_start((addr<<1) + TWI_WRITE);
        twi_stop();
        /* Test result from I2C bus. If it is 0 then move to ACK state, 
         * otherwise move to IDLE */
         
         if (result==0)
              state = STATE_ACK;
              
         else
              state = STATE_IDLE;
        
        break;

    // A module connected to the bus was found
    case STATE_ACK:
        // Send info about active I2C slave to UART and move to IDLE
    
    	itoa(addr, uart_string, 10);
    	uart_puts_P("Found device at address: ");
    	uart_puts(uart_string);
    	uart_puts_P("\r\n");
    	state = STATE_IDLE;
    
        break;

    // If something unexpected happens then move to IDLE
    default:
        state = STATE_IDLE;
        break;
    }
}
```

2. (Hand-drawn) picture of I2C signals when reading checksum (only 1 byte) from DHT12 sensor. Indicate which specific moments control the data line master and which slave.

  ![IMG-3791](https://user-images.githubusercontent.com/91128800/141953673-c1102fd2-991a-49e0-af53-10e95918ff29.jpg)


### Meteo station

Consider an application for temperature and humidity measurement and display. Use combine sensor DHT12, real time clock DS3231, LCD, and one LED. Application display time in hours:minutes:seconds at LCD, measures both temperature and humidity values once per minut, display both values on LCD, and when the temperature is too high, the LED starts blinking.

1. FSM state diagram picture of meteo station. The image can be drawn on a computer or by hand. Concise name of individual states and describe the transitions between them.

   ![IMG-3793](https://user-images.githubusercontent.com/91128800/141962181-f4e30105-c986-4943-90fb-d26cd16328d8.jpg)

