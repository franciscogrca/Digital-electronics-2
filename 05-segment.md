
# Lab 5: FRANCISCO ABELARDO GARCÍA AVILÉS

Link to your `Digital-electronics-2` GitHub repository:

   [https://githu/...](https://github.com/...)


### 7-segment library

1. In your words, describe the difference between Common Cathode and Common Anode 7-segment display.
   * CC SSD: All cathodes connected to node os log. 0, GND and control of individual segments a, ..., g, DP applying log. 1 on anode (includ. limiting resistor).
 
   * CA SSD: All anodes to log. 1 and control of segments a, ..., g, DP applying log. on anode (includ. limiting resistor).

2. Code listing with syntax highlighting of two interrupt service routines (`TIMER1_OVF_vect`, `TIMER0_OVF_vect`) from counter application with at least two digits, ie. values from 00 to 59:

```c
/**********************************************************************
 * Function: Timer/Counter1 overflow interrupt
 * Purpose:  Increment counter value from 00 to 59.
 **********************************************************************/
ISR(TIMER1_OVF_vect)
{
    
	static uint8_t tens = 0; 
   static uint8_t units = 0;
   
   units++;
   
   
	if (units>9)
	{
		units = 0;
      tens++;
    
      
	}
   
	else if (units>5)
	{
		tens = 0;
	}

}
```

```c
/**********************************************************************
 * Function: Timer/Counter0 overflow interrupt
 * Purpose:  Display tens and units of a counter at SSD.
 **********************************************************************/
ISR(TIMER0_OVF_vect)
{
   static uint8_t tens = 0; 
   static uint8_t units = 0;
   static uint8_t pos = 0;
    
   pos++; 
    
   if (pos>1){ 
   
   pos=0;
   SEG_update_shift_regs(units,pos);
   
   }
   
   else{
   
   SEG_update_shift_regs(tens,pos);
   
   }

}
```

3. Flowchart figure for function `SEG_clk_2us()` which generates one clock period on `SEG_CLK` pin with a duration of 2&nbsp;us. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

![CamScanner 10-25-2021 21 17-1](https://user-images.githubusercontent.com/91128800/138756645-dcf6de1a-c686-4ec4-87d6-b324350e854a.jpg)



### Kitchen alarm

Consider a kitchen alarm with a 7-segment display, one LED and three push buttons: start, +1 minute, -1 minute. Use the +1/-1 minute buttons to increment/decrement the timer value. After pressing the Start button, the countdown starts. The countdown value is shown on the display in the form of mm.ss (minutes.seconds). At the end of the countdown, the LED will start blinking.

1. Scheme of kitchen alarm; do not forget the supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values.

   ![your figure]()
