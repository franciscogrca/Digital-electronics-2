# Lab 7: FRANCISCO ABELARDO GARCÍA AVILÉS


[My Github Repository](https://github.com/franciscogrca/Digital-electronics-2)


### Analog-to-Digital Conversion

1. Complete table with voltage divider, calculated, and measured ADC values for all five push buttons.

   | **Push button** | **PC0[A0] voltage** | **ADC value (calculated)** | **ADC value (measured)** |
   | :-: | :-: | :-: | :-: |
   | Right  | 0&nbsp;V | 0   | 0 |
   | Up     | 0.495&nbsp;V | 101 | 99 |
   | Down   |   1.203&nbsp;V    |  246   | 257 |
   | Left   |    1.970&nbsp;V   |  403   | 410 |
   | Select |    3.182&nbsp;V   |   651  | 640 |
   | none   |    5&nbsp;V   |   1023  | 1023 |

2. Code listing of ACD interrupt service routine for sending data to the LCD/UART and identification of the pressed button. Always use syntax highlighting and meaningful comments:

```c
/**********************************************************************
 * Function: ADC complete interrupt
 * Purpose:  Display value on LCD and send it to UART.
 **********************************************************************/
ISR(ADC_vect)
{
    uint16_t value = 0;
    char lcd_string[4] = "0000";

    value = ADC;                  // Copy ADC result to 16-bit variable
    
    // Clear previous value
    lcd_gotoxy(8,0);
    lcd_puts("    ");
    
    //Put new value to LCD
    itoa(value, lcd_string, 10);  // Convert decimal value to string
    lcd_gotoxy(8,0);
    lcd_puts(lcd_string);
    
    // Send the same value to UART
    uart_puts(lcd_string);
    uart_puts("  ");
       
    // Display value in hexa
    itoa(value, lcd_string, 10);
    lcd_gotoxy(8, 0);
    lcd_puts(lcd_string);

    // Display what push button was pressed
    itoa(value, lcd_string, 16);
    lcd_gotoxy(13, 0);
    lcd_puts(lcd_string);

    uart_puts(lcd_string);
    uart_putc('\n');
    uart_putc('\r');
   
}
```


### UART communication

1. (Hand-drawn) picture of UART signal when transmitting three character data `De2` in 4800 7O2 mode (7 data bits, odd parity, 2 stop bits, 4800&nbsp;Bd).

  ![uart signalbuenon-1](https://user-images.githubusercontent.com/91128800/140737030-844c3530-f8a6-40a8-a7e5-e96844b6aeaf.jpg)


2. Flowchart figure for function `get_parity(uint8_t data, uint8_t type)` which calculates a parity bit of input 8-bit `data` according to parameter `type`. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

  ![IMG-3497](https://user-images.githubusercontent.com/91128800/140805145-d81f4adf-252d-47b6-b7cc-fce42fc78c1c.jpg)

![IMG-3499](https://user-images.githubusercontent.com/91128800/140805807-ceec8aa0-e03b-4b9b-9b06-189160d989ea.jpg)


### Temperature meter

Consider an application for temperature measurement and display. Use temperature sensor [TC1046](http://ww1.microchip.com/downloads/en/DeviceDoc/21496C.pdf), LCD, one LED and a push button. After pressing the button, the temperature is measured, its value is displayed on the LCD and data is sent to the UART. When the temperature is too high, the LED will start blinking.

1. Scheme of temperature meter. The image can be drawn on a computer or by hand. Always name all components and their values.

   ![Captura de pantalla 2021-11-09 105513](https://user-images.githubusercontent.com/91128800/140902620-d5e45d91-9c06-43b9-ab19-75a123568fb5.png)

