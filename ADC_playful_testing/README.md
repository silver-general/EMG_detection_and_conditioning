I'm gonna try to do some little excercise with progressive difficulty to understand how ADC and memory are handled. I will use mostly a LED output to debug.

The ideas that come to my mind are:  
#### idea 1  
launch the ADC. read a value (0 to 5 Volts. 8 bit resolution. 19.5mV/level). Depending on the intensity of the signal (amplitude divided in 5 slots, for example), have a different response intensity.  
the response could be a) output a voltage on portB pin 0,1,2,... OR b) use PWM to drive a LED, that could be cooler. do both.

#### idea 2  
launch ADC. detect values applied to an input pin. write those values on the stack. then stop ADC, read the values and output them into a pin.

MANY issues will arise, mostly about timing. 
