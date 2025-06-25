---
title: "Nintendo Arduino Keytar"
date: 2019-06-29
draft: false
description: "Nintendo Arduino Keytar"
tags: ["Nintendo", "NES", "Arduino", "keytar", "diy", "homemade instrument"]
---
While browsing through Cigar Box Guitar groups on Facebook, I kept coming across this post about a NES that had been turned into a 6 string guitar. I thought it was the coolest idea, and decided I wanted to make one. But then I thought…this has already been done. What else can I do with it? I had also been thinking about making an instrument with an Arduino, and bam! an idea was born. What if I created an instrument that looked like a guitar, with the NES as the body, but made the sounds with an Arduino?

From my dabbling with this microcontroller I knew that I could produce simple tones, which are the types of tones that the most primitive 8-bit arcade games from the 80’s sounded like. I also thought I could use a soft potentiometer along the neck of this instrument to represent the notes. But how would I strum the instrument? I chose to add an arcade button to toggle the sound on and off when pressed. While I was at it, I added two other buttons to raise and lower the octave. Finally I added one last button to alternate between fretted mode and slide mode. When in fretted mode, there are discreet parts of the neck that make certain notes, like a fretted guitar. If you run your finger up and down the neck in this mode you get only the notes on a typical guitar. Switching to slide mode changes it so that you get all the notes and everything in between, like if you were playing a guitar with a slide. I wired the Arduino to the NES power button so it can be turned on and off.

This was a fun build that was a bit of a departure for me. I got to flex my coding muscles a bit, which I hadn’t done in some time.

{{< youtube MO_Qi6R-WdM >}}
{{< youtube 7tjgVzbcsWU >}}
{{< youtube Uvp20X3Wb_o >}}
{{< youtube E3ZXLnPtF04 >}}

{{< figure src="chiptar06.JPG" caption="The finished product" >}}
{{< figure src="chiptar05.JPG" caption="Headstock made from the circuit board" >}}
{{< figure src="chiptar02.JPG" caption="" >}}
{{< figure src="2019-06-29 09.26.58.jpeg" caption="Fret markers on the side of the neck" >}}
{{< figure src="2019-06-29 06.08.31.jpg" caption="Laying out the components" >}}
{{< figure src="2019-05-16 19.57.39.jpg" caption="Soldering the components" >}}
{{< figure src="2019-04-28 08.23.03.jpeg" caption="Testing the soft potentiometer" >}}
