---
layout: post
title: OSX Lion Colour Sampling using DigitalColor Meter
date: 2012-01-05 14:38
comments: true
categories:
- web development
- mac
---

Previously when I was running Mac OSX Snow Leopard I would use the built
in tool 'DigitalColor Meter' to grab RGB values from my screen. Using the
tool is is very quick to grab colours from websites, photoshop files,
anything really.

When I upgraded to OSX Lion and opened the colour meter for the first
time I realised that it had changed and I could no longer quickly grab
colour values to use. I realised though by changing one of the menu
settings I could get back the previous functionality; here's how:

<!-- more -->

First open the DigitalColor Meter app, you can find it using Spotlight.

![Opening the Application using Spotlight](/images/blog/digital_color_meter/meter_1.png)

It looks like this, you'll notice that the displayed values are in
absolute RGB 0-255 values.

![DigitalColor Meter Application](/images/blog/digital_color_meter/meter_2.png)

Select `View` => `Display Values` => `As Hexadecimal`

![Setting the display value to hexadecimal](/images/blog/digital_color_meter/meter_3.png)

Now you can sample a colour simply by hovering over the colour you want.
Once you are ready press `Command` + `Shift` + `C`. It should copy the
hexadecimal colour to your clipboard.

You should be able to notice it is copying the colour as the Color item
on the top menu will highlight monetarily.

![Setting the display value to hexadecimal](/images/blog/digital_color_meter/meter_4.png)
