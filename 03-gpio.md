# Lab 3: Francisco Abelardo García Avilés


   [franciscogrca/Digital-electronics-2/03-gpio](https://github.com/franciscogrca/Digital-electronics-2/blob/main/03-gpio.md)


### Data types in C

1. Complete table.

| **Data type** | **Number of bits** | **Range** | **Description** |
| :-: | :-: | :-: | :-- | 
| `uint8_t`  | 8 | 0, 1, ..., 255 | Unsigned 8-bit integer |
| `int8_t`   | 8 | -128 to 127 | Signed 8-bit integer |
| `uint16_t` |16  | 0 to 65,535 | Unsigned 16-bit integer|
| `int16_t`  | 16 | -32,768 to 32,767 | Signed 16-bit integer |
| `float`    | 32 | -3.4e+38, ..., 3.4e+38 | Single-precision floating-point |
| `void`     |  |  | Indicates that the function does not return a value |


### GPIO library

1. In your words, describe the difference between the declaration and the definition of the function in C.
   
   * Function declaration: tells the compiler about a function´s name, return type, and parameters.
   * Function definition: provides the actual body of the function.

2. Part of the C code listing with syntax highlighting, which toggles LEDs only if push button is pressed. Otherwise, the value of the LEDs does not change. Use function from your GPIO library. Let the push button is connected to port D:

```c
    // Configure Push button at port D and enable internal pull-up resistor
    
/* Defines -----------------------------------------------------------*/
#define LED_GREEN   PB5     // AVR pin where green LED is connected
#define BLINK_DELAY 500
#ifndef F_CPU
# define F_CPU 16000000     // CPU frequency in Hz required for delay
#endif

/* Includes ----------------------------------------------------------*/
#include <util/delay.h>     // Functions for busy-wait delay loops
#include <avr/io.h>         // AVR device-specific IO definitions
#include "GPIO.h"           // GPIO library for AVR-GCC

int main(void)
{
    // Infinite loop
    while (1)
    {
        // Pause several milliseconds
        _delay_ms(BLINK_DELAY);

       GPIO_toggle(&PORTB, LED_GREEN);
       
       GPIO_config_input_pullup(&DDRB, LED_GREEN)
    }
     
     return 0;
}    
```


### Traffic light

1. Scheme of traffic light application with one red/yellow/green light for cars and one red/green light for pedestrians. Connect AVR device, LEDs, resistors, one push button (for pedestrians), and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values!

  
![lab03traffic](https://user-images.githubusercontent.com/91128800/136911368-a72dd887-2099-4cb2-92bb-5d79fd384920.png)

