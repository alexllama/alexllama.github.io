---
title: "Zoom Mute Button"
date: 2020-10-29
draft: false
description: "Zoom Mute Button"
tags: ["zoom", "digispark", "mute"]
---

Zoom became the way to communicate with coworkers during the COVID pandemic in 2020. It quickly became apparent that there needed to be a way to mute yourself easily without having to navigate to the app and click the Mute button. Since this feature has a keyboard shortcut, it was easy to create a button to do this. I used a Digispark microcontroller. It's very small and only a couple of bucks, so it was perfect for this. I added a red LED to indicate when Mute was enabled. As a bonus feature, holding the button down will drop from the meeting. You can see the code in my [GitHub repo](https://github.com/alexllama/Zoom-Mute).

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