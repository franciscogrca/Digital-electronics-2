# Lab 4: Francisco Abelardo García Avilés


   [My GitHub repository](https://github.com/franciscogrca/Digital-electronics-2)


### Overflow times

1. Complete table with overflow times.

| **Module** | **Number of bits** | **1** | **8** | **32** | **64** | **128** | **256** | **1024** |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| Timer/Counter0 | 8  | 16u | 128u | -- | 1m | -- | 4m | 16m |
| Timer/Counter1 | 16 |  4m   |   33m   | -- | 262m | -- | 1sec | 42sec |
| Timer/Counter2 | 8  |  16u   |   128u   |  512u  | 1m |  2m  | 4m | 16m |


### Timer library

1. In your words, describe the difference between common C function and interrupt service routine.
   * Function
   * Interrupt service routine

The main difference between a function and interrupt is what is known as context. A function runs within the context of your main program. An interrupt runs within the context of the interrupt handler

2. Part of the header file listing with syntax highlighting, which defines settings for Timer/Counter0:

```c
/**
 * @name  Definitions of Timer/Counter0
 * @note  F_CPU = 16 MHz
 */
/** @brief Stop timer, prescaler 000 --> STOP */
#define TIM0_stop()           TCCR0B &= ~((0<<CS02) | (0<<CS01) | (0<<CS00));
/** @brief Set overflow 16us, prescaler 001 --> 1 */
#define TIM0_overflow_16us()   TCCR0B &= ~((0<<CS02) | (0<<CS01)); TCCR0B |= (0<<CS00);
/** @brief Set overflow 128us, prescaler 010 --> 8 */
#define TIM0_overflow_128us()  TCCR0B &= ~((0<<CS02) | (0<<CS00)); TCCR0B |= (0<<CS01);
/** @brief Set overflow 1ms, prescaler 011 --> 64 */
#define TIM0_overflow_1ms() TCCR0B &= ~(0<<CS02); TCCR0B |= (0<<CS01) | (0<<CS00);
/** @brief Set overflow 4ms, prescaler 100 --> 256 */
#define TIM0_overflow_4ms()    TCCR0B &= ~((0<<CS01) | (0<<CS00)); TCCR0B |= (0<<CS02);
/** @brief Set overflow 16ms, prescaler // 101 --> 1024 */
#define TIM0_overflow_16ms()    TCCR0B &= ~(0<<CS01); TCCR0B |= (0<<CS02) | (0<<CS00);
/** @brief Enable overflow interrupt, 1 --> enable */
#define TIM0_overflow_interrupt_enable()  TIMSK0 |= (0<<TOIE0);
/** @brief Disable overflow interrupt, 0 --> disable */
#define TIM0_overflow_interrupt_disable() TIMSK0 &= ~(0<<TOIE0);
```

3. Flowchart figure for function `main()` and interrupt service routine `ISR(TIMER1_OVF_vect)` of application that ensures the flashing of one LED in the timer interruption. When the button is pressed, the blinking is faster, when the button is released, it is slower. Use only a timer overflow and not a delay library. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

 ![IMG-2043](https://user-images.githubusercontent.com/91128800/137816968-9700278f-5a02-45aa-9779-f584d252de4e.jpg)

![IMG-2042](https://user-images.githubusercontent.com/91128800/137816970-3153ad08-2da3-48aa-9822-4752354d8448.jpg)


### Knight Rider

1. Scheme of Knight Rider application with four LEDs and a push button, connected according to Multi-function shield. Connect AVR device, LEDs, resistors, push button, and supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values.

 ![Captura de pantalla 2021-10-18 173118](https://user-images.githubusercontent.com/91128800/137763381-992f8849-e1bc-4c62-b6d3-805c6328211e.png)

