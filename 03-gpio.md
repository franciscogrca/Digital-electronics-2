# Lab 3: Francisco Abelardo García Avilés

Link to your `Digital-electronics-2` GitHub repository:

   [franciscogrca/Digital-electronics-2/03-gpio](https://github.com/franciscogrca/Digital-electronics-2/blob/main/03-gpio.md)


### Data types in C

1. Complete table.

| **Data type** | **Number of bits** | **Range** | **Description** |
| :-: | :-: | :-: | :-- | 
| `uint8_t`  | 8 | 0, 1, ..., 255 | Unsigned 8-bit integer |
| `int8_t`   | 8 | -128 to 127 |  |
| `uint16_t` |16  | 0 to 65,535 |  |
| `int16_t`  | 16 | -32,768 to 32,767 |  |
| `float`    | 32 | -3.4e+38, ..., 3.4e+38 | Single-precision floating-point |
| `void`     |  |  | Indicates that the function does not return a value |


### GPIO library

1. In your words, describe the difference between the declaration and the definition of the function in C.
   
   * Function declaration: tells the compiler about a function´s name, return type, and                            parameters.
   * Function definition: provides the actual body of the function.

2. Part of the C code listing with syntax highlighting, which toggles LEDs only if push button is pressed. Otherwise, the value of the LEDs does not change. Use function from your GPIO library. Let the push button is connected to port D:

```c
    // Configure Push button at port D and enable internal pull-up resistor
    // WRITE YOUR CODE HERE

    // Infinite loop
    while (1)
    {
        // Pause several milliseconds
        _delay_ms(BLINK_DELAY);

        // WRITE YOUR CODE HERE
    }
```


### Traffic light

1. Scheme of traffic light application with one red/yellow/green light for cars and one red/green light for pedestrians. Connect AVR device, LEDs, resistors, one push button (for pedestrians), and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values!

  ![Traffic lights](https://user-images.githubusercontent.com/91128800/136909069-ab108eda-c134-4ca2-a9df-fd8c25468e04.png)

