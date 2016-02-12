---
title:  "Ov7670"
subtitle: "CMOS camera"
author: "Akash Salow"
avatar: "img/authors/salow.jpg"
image: "img/foe.jpg"
date:   2015-04-22 12:12:12
---

### Getting started
I’m pretty new to electronics, and I’m learning new stuff every day. On my most recent attempt at breathing life into the wretched thing, my attention got directed towards a feature I had not even considered before – the XCLK pin. This pin labeled “external clock”, always seemed to me like it was something optional, as I’ve gotten used to all my other toys having internal RC oscillators, or no need for oscillators. But no, in this case it’s not optional, and my oversight seems so obvious now!

I’ve read pretty much every document available on the internet about the ov7670 sensor, but to this day, I’m not sure it’s clearly stated anywhere that feeding the XCLK is an important step  to getting the ov7670 up and running. It’s probably listed in every schematic out there, but my newbie mind ignored it.

### Working on
Next step was to output the data via UART at more convenient speeds. Initially I didn’t seem to be able to pump the data to my computer at speeds more than ~57600. Somewhere the data got buffered, and when it buffered enough, it went nuts. So I adjusted the serial protocol a little, so the client sends commands to request lines one at a time, and the lpcxpresso responds with data. This keeps both parties happy about the rate of data flowing, and I was able to increase the baudrate to 921600.

Now I was able to view a new image from the camera every 1-2 seconds. This almost feels like watching a video instead of a slideshow :) I could do some tricks to get faster framerates, but actually I won’t bother. My initial thoughts with the camera were to use it for still images taken on request, and to transfer them wirelessly via XBee, so in future I’ll use the camera at a much slower pace.

In case someone reads this page one day, looking for advise with the ov7670, I’ll list some notes here that might be useful:

    Needs a clock source
    i2c is dodgy, I had to add some delay to read routines
    different versions exist on ebay, some take 2.8V instead of 3.3V, and some have FIFO

