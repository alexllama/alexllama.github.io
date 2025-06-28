---
title: "LED Macro Pad"
date: 2025-01-31
draft: false
description: "LED Macro Pad"
tags: ["macro pad", "teensy", "lego"]
---

Macro Pads are great for running programs or performing other actions at the touch of a button. They sell some on Amazon, but from the reviews I didn't get the impression that I could do a lot of customizing, particularly on Linux, which is where I wanted to use one. So I made one with a Teensy microcontroller, 6 buttons and a rotary encoder to control the volume. You can get a copy of the code in my [GitHub repo](https://github.com/alexllama/MacroPad).

{{< figure src="featured.jpg" caption="The finished product" >}}

The buttons are laid out as follows:
{{< figure src="layout.jpg" >}}
Button names:
- RE - Rotary Encoder (Volume)
- MT - Mute
- LD - Left Desktop
- RD - Right Desktop
- PP - Play/Pause
- PT - Previous Track
- NT - Next Track

After adding all the buttons for controlling media, I had two buttons left over. I used those to toggle between virtual desktops.

{{< figure src="2025-01-31 22.02.40.jpg" caption="Easy access next to my laptop" >}}

Here's a video showing it at work
{{< youtube fMsZvGEkdMU >}}