Using a microcontroller requires carefully handling all its limitations.  
The tiny85 has a 10bitADC, but for simplicity 8 bit ADC can be used (otherwise you must handle high and low byte for a single data point.  
Frequency of ADC depends on the program speed. Using assembly one can determine what happens when with a precision of a nanosecond (some instructions require 2 ns, e.g. rjmp. interrupts also change timing).

What will the tiny85 do?  
- start the ADC, then acquire data every X seconds, where X is the time it takes in the loop from one acquisition to the other.
- data has to be stored somewhere, because using only registers allow something like 25 acquisition. see memory section for AVR risc MCU. it will be SRAM.  

How do you detect muscle activity?  
When the muscle activates, EMG signal will be mostly a 40-50 Hz, and in the surfare there will be 10mV peak-peak (5mV rectified) to be detected.
- amplitude and frequency will vary with the muscle groups. see an atlas about electrode placement for the correct expectations.

what will the MCU do?  
I guess it will take samples for a while, then do calculations to find the average amplitude, then if over a threshold it'll activate something, then start over.

#### things to be taken into account:
- sampling rate? min, max?
- how many sample to take?

## Testing Ideas
Since I am not an expert, I will play a bit with the attiny85 ADC to make some simple projects, then increase the complexity gradually.  
See the file "ADC_conversions_playful_testing"
