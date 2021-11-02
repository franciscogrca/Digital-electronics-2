# Lab 6: FRANCISCO ABELARDO GARCÍA AVILÉS


[My Github Repository](https://github.com/franciscogrca/Digital-electronics-2)


### LCD display module

1. In your words, describe what ASCII table is.
   
   * ASCII: The ASCII table contains letters, numbers, control characters, and other symbols. Each character is assigned a unique 7-bit code. ASCII is an acronym for American Standard Code for Information Interchange.

2. (Hand-drawn) picture of time signals between ATmega328P and LCD keypad shield (HD44780 driver) when transmitting three character data `De2`.

   ![timer](https://user-images.githubusercontent.com/91128800/139810873-cb3d2a8b-76f6-4c00-b4a6-fb56ab4d4845.jpg)



### Stopwatch

1. Flowchart figure for `TIMER2_OVF_vect` interrupt service routine which overflows every 16&nbsp;ms but it updates the stopwatch LCD approximately every 100&nbsp;ms (6 x 16&nbsp;ms = 100&nbsp;ms). Display tenths of a second and seconds `00:seconds.tenths`. Let the stopwatch counts from `00:00.0` to `00:59.9` and then starts again. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

   ![IMG-3038](https://user-images.githubusercontent.com/91128800/139670370-0ebeaf61-953d-4b7f-b4ee-2bc89ad2229c.jpg)



### Custom characters

1. Code listing with syntax highlighting of two custom character definition:

```c
/* Variables ---------------------------------------------------------*/
// Custom character definition
uint8_t customChar[16] = {
    0b11011,
    0b10001,
    0b11011,
    0b00000,
    0b10001,
    0b11011,
    0b10001,
    0b10101,
    0b11011,
    0b10001,
    0b11011,
    0b00000,
    0b10001,
    0b11011,
    0b10001,
    0b10101

};
```


### Kitchen alarm

Consider a kitchen alarm with an LCD, one LED and three push buttons: start, +1 minute, -1 minute. Use the +1/-1 minute buttons to increment/decrement the timer value. After pressing the Start button, the countdown starts. The countdown value is shown on the display in the form of mm.ss (minutes.seconds). At the end of the countdown, the LED will start blinking.

1. Scheme of kitchen alarm; do not forget the supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values.

   

![kitchenbueno](https://user-images.githubusercontent.com/91128800/139804231-bc33ce10-adfe-44cf-91ae-05ec53f5db8d.png)
