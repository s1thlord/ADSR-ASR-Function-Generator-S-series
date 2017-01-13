##S1 Series Envelope generator 

By Chris Holder Any comments or quiries please E:mail the author <Chris.holder@mail.com>

##Introduction 

This project is the second module to be made for the S-series. This module is going to provide envelope generation and will constitute the Dual oscillator with output control making these two units the bare minimum requirement for the system to work. As with the dual oscillator found at this address <https://github.com/s1thlord/S-series> is also a continuation of the software patches written in pure data emulating three modules of the Buchla 200 series this software can be found at <https://github.com/s1thlord/7MU009-Idon> .
The original Pure-Data patch was written to be an authentic recreation of 1970’s modular gear however for this project the idea is simply to make an updated version of the unit functionality and to make the most use from the Axoloti core circuit working within the board limitations. However to consider the full desired functionality of the module a look at the current units available was undertaken (a collection of envelope generators is shown in Fig 1).

 
![buchla281](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/Screen%20Shot%202016-12-09%20at%2013.38.12.png)

![buchla281](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/Screen%20Shot%202016-12-09%20at%2013.43.36.png)

![buchla281](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/Screen%20Shot%202016-12-09%20at%2013.50.17.png)

![buchla281](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/Screen%20Shot%202016-12-09%20at%2014.04.24.png)
 
Fig 1 A selection of Envelope Generator modules available at this time 2016.


Upon considering the current market place for envelope generators it has been considered to make the unit ADSR (Attack, Decay, Sustain, Release), as this approach seems to be the most popular control method amongst these types of units at the present time. 



##Project start specifications 

•	Dual ADSR envelope generator.
•	Externally triggered
•	









##Software concept

Starting this project with the Axoloti patching software has been somewhat easier than with the dual oscillator due to being more comfortable with the available objects within the software. After consideration into what functions the unit should have and also wishing to copy at least some of the available functions that are present on the Pure-Data version (shown in Fig 2). 


![buchla281](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/pure%20data%20buchla%20envat%2013.44.36.png)


Fig 2 Control face of Pure-Data patch emulating a Buchla 280 Envelope Generator.

The first part of the software design to be implemented into a test patch as with the dual oscillator was the main function requirement of the module. This area of Digital Signal Processing (DSP) seems to be a well-trodden ground for the author of the Axoloti software with various similar objects being available. As we can see from Fig 3 which shows the implementation of the ADSR patch only one object is needed to achieve this function, much simpler that the Pure-Data version (shown in Fig 4) to implement however time values are easily attenuated in the PD software. The issue with the Axoloti version here akin to the dual oscillator pitch control etc. It is a locked in parameter over the attack and decay times which seems to affect all versions so far created by the factory or the community, unless you are fully versed in XML machine code language it may then be possible to change these values, however even then it may not be possible due to the core software being scaled to it’s attached hardware.         



![buchla281](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/ADSR%20test%20at%2021.53.58.png)


Fig 3 Test abstraction for ADSR function.


![buchla281](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/pure%20data%20rampt%2013.45.46.png)

Fig 4 Pure-Data Attack control patch.


After completing the first ADSR (attack, decay, sustain, release) patch a way was sought to lengthen the attack and release slops also it was considered a desired notion to have externally triggered attack and release to achieve this separate objects where needed to control both linear ramps. Shown in Fig 5 a line hold decay object was used to give a linear ramp and also an automatic sustain as long as a user holds the initial trigger open be that a musical keyboard or other such device. The release is governed by a hold decay object which when triggered gives a downwards linear ramp. At this time however no way has been found to amend the attack decay times governing the ramps.


![buchla281](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/AR%20test%20patch%20%2014.54.46.png)


Fig 5 Axoloti abstraction showing trigger able attack, release gates.

A choice was now left to the project weather to have ADSR or ASR as its envelope function. The reason only one of these methods is being chosen is down to a hardware restriction whereby only two audio output channels are available to use on the Axoloti core board hence a dual envelope, rather than a quad output as was done in Pure-Data modelling of the Buchla 200 series envelope (shown in Fig 2). Making the decision to house the ASR function as the main parameter of the unit mainly due to its extra functionality with CV able inputs was a clear choice. However once this choice had been made and the test abstraction put into a working software model, one particular point had to be noted which was the extreme amount of CPU resource still available to use as the overall model was running at about 9% of available load. This lack of CPU utilisation was considered to be a waste of expensive Axoloti resource. 
To utilise at least some of the CPU availability it was considered to add functions to the module that would be useful to the overall function that of envelope generation. It is also being considered to set functions that will make this unit have more individual character in order to make it stand out when juxtaposed against other manufactured units of the same calibre. To aid in these considerations the author looked back at the Buchla 281 envelope in a hope to inspire some new direction in regards development of the module.
The first initial update to the unit’s functions has been a debate on weather to attempt some form of quad envelope functionality. Therefore adding the original ADSR test abstraction to the mix. The addition of ADSR in another two channels means that they must share audio inputs with the ASR already in operation however with the implementation of separate triggers for each envelope it should be possible with the correct audio output configuration to make use of all four independently. This function would add 2 extra 6.35mm jack sockets to the interface, which can be added to the layout design already in consideration. Another addition inspired from the Buchla envelope concerning triggers is the ability to fire an output trigger upon the release of the envelope. Which in turn will add another four 6.35mm jack sockets to the interface although adding a small cost to the unit and a small redesign of the interface it is felt that the added operandi more than make up for this small expense. Upon consideration of the audio output of the module, it has been a thought to add cross-faders over each channel to control the envelope outputs. Whereby careful setting of the envelope release times should allow a user to access all four envelopes over both channels.
One function also under debate for an added upgrade to the project is the addition of an OR logic function over the triggers also inspired by the Buchla unit. 
To correctly model this function the Buchla users manual was used to understand this function which is described as follows “Generators A and B operate in tandem to provide more complex envelopes.”(Buchla owers manual 2005). This is achieved by the release of gate A triggering the attack of gate B. 
However this function is a get round due to needing each audio source to have a separate channel for the rest of the Buchla OR functions to operate correctly. 
The missing function from this module is as stated “As before, a pulse applied to the A input triggers the attack phase of A. When A's attack is completed, B begins its attack while A stays high. When B's attack is complete, A begins its decay while B stays high. And finally, when A's decay is completed, B begins its decay.”(Buchla, 2005).
The reason for this exclusion is the audio crossfade will mix the final outputs of each gate, which is probably an undesired function as the user has patched separate gates over the source. 
This function was never added to the Pure-Data version Due to CPU load being to great when all three modules where run simultaneously from the same laptop. However here we have more than enough CPU power left over to run this added function. 
Having added a mathematical operandi to the module in the shape of the OR function this update Gave the author an inspiration to strike the S1 envelope generator away from the Buchla in terms of design. The thought here was to add more maths capabilities to the module. By changing the release response curve of the each envelope by adding to the linear response with logarithmic and exponential modes activated by the flick of a switch. Another consideration for this project is also based on mathematical functions only this time on the incoming signal to the envelope. Including the function to each of the two channels the ability to subtract and add the signals together. The new abstraction with all the updated functions is shown in fig 6




![buchla258](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/finalenvelope%20version.png)

Fig 6  Axoloti patch for S1 series envelope generator.   
     






##Interface design 

After completing the software functionality for this unit, the interface design can be based upon the controllers needed. 
The interface design for this unit will use the same approach used by the dual oscillator. Using a left to right approach to the controller layout it is hoped that a user will not only find this an intuitive control method when the module is used in conjunction with other modules from the series but also using the same design concept will give uniformity to the whole series. The design for this project is shown below in Fig 7.


![](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/IMG_20170109_120533%20copy.jpg)
Fig 7  ADSR  envelope generator interface layout.


Having added new functions to the unit a new layout design was needed to reflect these changes (shown in Fig 8)



![](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/IMG_20170109_120647%20copy.jpg)

Fig 8   Quad envelope update concept interface layout.  

Here will be reflected the interface build in picture format.

![](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/IMG_20170111_213152.jpg)
![](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/IMG_20170112_153939.jpg)









##Hardware design

Having done all of the ‘leg’ work as far as interface controllers is concerned in regards the S1 series was all completed in the oscillator build and is talked about in length in the hardware connection chapter. Hence this chapter will just blog the build of the envelope generator.
The following photographs (Fig 10) will give a pictorial blog of the rest of the hardware construction.


![](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/IMG_20161231_202237.jpg)
![](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/IMG_20170101_121220.jpg)
![](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/IMG_20170101_144745.jpg)
![](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/IMG_20170101_181125.jpg)
![](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/IMG_20170111_112606.jpg)
![](https://github.com/s1thlord/ADSR-ASR-Function-Generator-S-series/blob/master/IMG_20170113_111722.jpg)

Fig 10 shows pictures from blank matrix board to full circuit board inclusion.




##Final Specifications
•	Quad ADSR/ AR Envelope generator
•	Mathematical functions +/- or
•	Linear, logarithmic and exponential release response
•	Midi and 10 volt trigger compatible
•	Dimensions 3U compatible HP 30 




##Evaluation
This evaluation has also used the approach taken with the dual oscillator by comparing both the Idon software and hardware equivalents. The original Idon software was loosely based on the Buchla 281 envelope generator being capable of the fundamental operations of the hardware. Comparing the Idon software to the S1 series envelope function generator, all of the primarily functions are available however the S1 series carries extra functionality. These extra functions are due to the software development of the unit discussed in depth in the software concept chapter. 
When the S1 envelope generator is juxtaposed against other hardware counterparts. These include such modules as the Make Noise Maths and the Buchla 281 envelope generator alongside the Doepfer A104 ADSR. A couple of disadvantages to the S1 become apparent. The first issue is concerned with the release time of the units ADSR and AR envelopes. All of the hardware models stated and also the Idon software share a release time of 10-20 seconds however the maximum possible time for the S1 is 5 seconds due to software object restrictions. This maximum release time could be argued to be more musically useful however if the gates have been set for more complex patterns this extra time would have been a useful feature. 
The second disadvantage to the S1 envelope is the limitation of two audio input and output channels. Whereas the Buchla and the Make Noise modules have four independent audio channels, as discussed earlier in the software concept chapter this is the reason why the full Buchla OR function could not be added. The purpose of the crossfade function over both audio outputs was the author’s answer to achieving at least some of the functions available to a full quad envelope.
Despite these two shortcomings of the S1 series envelope, the module itself as introduction level hardware has some powerful functions with which to inflict upon an incoming audio signal. Coupled with the compatibility of the unit with popular modular synthesis 10-volt trigger designs and the capability of MIDI trigger input.    







##Resources

Buchla Associates 200e Users Guide, 2005.
Available at http://www.buchla.com/guides/200e_Users_ Guide.pdf




##Links


<https://github.com/s1thlord/7MU009-Idon>

<https://github.com/s1thlord/S-series>

