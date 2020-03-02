# EMG_detection_and_conditioning
Big Idea: design and build a system to acquire surface electromyographical signal and use it to control other systems (eg: robotic hand).

This is thought as a tutorial for people starting from scratch, as I too need to put my ideas in order.  

RULE #1: when in doubt, ask for help. join a makerspace, ask professors, students, stalk people on social media. the internet is full of good people that would help you and join you if you have a nice project. 

Acquiring biosignals require knowledge on many different topics, and if you dedicate your time to different subject you often end up knowing little of everything, that is both good and bad. That's why I'm putting everything public and hoping to get suggestions.

These are topics I personally found useful as a student at BSc in Biomedical Engineering. I recommend having knowledge in:
1. Electronics: how circuit work. frequency response of circuits. how operational amplifiers and filters work. I found incredibly useful the book "fundamentals of electric circuits". it's just a basic intro though, real life is harsh and require practical knowledge. ask students in Electronics and such.  
2. Biomedical instrumentation: you need to know how to physically connect electrodes to the circuit that will clean the signal, and how to determine values for operation amplifiers and electric components. a good knowledge of sEMG noise, artifacts, muscle physiology, skin impedance model is very helpful.  
3. Physiology: I read "introduction so sEMG" by Merletti and found it useful.  
4. signal analysis: this is what I lack. in order to tell a good signal from a bad one, you need to find features like the power transmitted or the average peak of the signal. also frequency analysis, if your MCU can handle that. 
...

SUPER RANDOM IDEAS:

1. Since the fft requires heavi calculations for a microcontroller such as ATtiny85, can I implement an analogue spectrum analyser? read more on this on:  
- https://sound-au.com/project136.htm
- https://electronics.stackexchange.com/questions/175068/designing-an-analog-circuit-that-fourier-transforms-or-laplace-transforms-an-inp
- https://www.researchgate.net/publication/224310162_Design_and_implementation_of_an_all-analog_fast-fourier_transform_processor 
