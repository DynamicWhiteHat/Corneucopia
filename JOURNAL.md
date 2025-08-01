---
title: "Corneucopia"
author: "DynamicWhiteHat"
description: "A Corne Based 42 Key Mechanical Keyboard"
created_at: "2025-06-04"
---

# Total time spent: 10 hours

## June 4: Ergogen Attempts

I decided that this time I wanted to design an ergonomic split keyboard, and a popular tool for designing such boards is Ergogen. Ergogen uses yaml files to generate a PCB based on the layout you give it. However, as this was my 
first time making an ergonomic keyboard, I had to look online for tutorials. After various attempts at following YouTube videos, I came across [this](https://flatfootfox.com/ergogen-part1-units-points/) tutorial series that 
explained Ergogen well. I used this tutorial to first create a set of keys that resembled the Corne layout, which looked like this:

<img width="421" height="373" alt="image" src="https://github.com/user-attachments/assets/3ad6539e-79f1-4d1d-8cf6-33b18d6383c8" />


Next, I added an outline, which took some time since the tutorial was making a reversible PCB, and thus only made an outline for one half of the board. Despite my many attempts, I was unable to figure out how to create
two outlines, one for the left and one for the right. I decided that I would also try to make a reversible as well, since I was unable to make a regular one. However, once I exported the PCB from Ergogen and opened it in
KiCad, everything looked different and the reversible footprints didn't make sense to me. I tried looking online for how it should be, but once again, I wasn't able to find information about this. I decided to make a PCB
the regular way using KiCad, since I have done that before. This was as far as I got with Ergogen:

<img width="631" height="488" alt="Screenshot 2025-06-04 104854" src="https://github.com/user-attachments/assets/0de32f78-f324-43c2-8b72-3ea83874545b" />

## Time Spent: 2 hours

## June 5: Restart using KiCad

Since I've made macropads and keyboards before in KiCad, making a schematic was relatively easy. I first started by selecting my MCU. I wanted the board to be wireless and have a display. Based on these parameters, I 
chose the Nice!Nano, since it comes from the same family as the Nice!View, and it supports wireless connectivity using ZMK. However, when buying the MCU, I will buy the Supermini NRF52840, which is a much cheaper
drop in replacement. I installed a popular keyboard library for KiCad called marbastlib and placed down the included Nice!Nano symbol.

Then, I added in the switches, which are chocs. I want this build to be low-profile, so chocs will fit this use case perfectly. I added 21 keys to each side, giving me a total of 42 keys. I also wanted to have per-key RGB,
so I added a neopixel for each switch. Then, I looked on typeractive.xyz for their power switches and found the JS102011CQN, an SPDT switch by C&K, as well as their reset button, which is manufactured by Panasonic. I imported these
symbols into my schematic and wired them up as well. Finally, I added a 2 pin JST connector for the battery and a 1x5 header for the OLED display. This is what my final schematic looks like:

<img width="1157" height="567" alt="image" src="https://github.com/user-attachments/assets/277a68a0-5d97-4113-bf9f-4fbfbf0bdf2e" />

## Time Spent: 1 hour

## June 6: PCB Work

I imported the PCB from the schematic, and I was blasted with various components. Although the schematic looked clean, the footprints from the marbastlib library had lots of drawings on them for placement, which made everythign
look larger than it actually was. I also imported the DXF outlines from Ergogen to help me with my key placement. I began placing the keys in their squares, which did require changing KiCad's rotation paramters, and once I was done, this is what it looked like:

<img width="1170" height="413" alt="Screenshot 2025-06-05 041530" src="https://github.com/user-attachments/assets/e9defc8c-f956-46b5-882e-54c9f5296239" />

Next, I placed the neopixels into their spots. The footprint for the switches had rectangles for where the neopixels should go, which made it easy to place.

<img width="480" height="455" alt="image" src="https://github.com/user-attachments/assets/5e036661-e152-4c2e-a1de-bc67d6231935" />

I placed the neopixels, once again using custom rotation paramters to fit the thunb cluster's rotation, and placed the last few remaining components as well. I also decided to add a rotary encoder to help it stand otu as a fully custom keybaord.
This is what my fully layed out PCB looks like:
<img width="784" height="614" alt="Screenshot 2025-06-05 041536" src="https://github.com/user-attachments/assets/e823bf8e-a3a4-42e5-84d1-81310974e453" />
<img width="522" height="379" alt="Screenshot 2025-06-05 041541" src="https://github.com/user-attachments/assets/ecaf366b-9080-41ce-9004-dfd156c7286f" />

Next, I moved onto routing. First, I routed the diodes together, which was relatively simple. However, after this, routing became much more difficult. When I tried to route the neopixels, the traces for the diodes would come in the way.
No matter how many times I tried rerouting both the neopixels and the diodes, I was unable to figure out the correct way to route them. I decided to consult my previous keyboard design and follow that wiring. This was my previous wiring:
<img width="1493" height="341" alt="Screenshot 2025-06-06 114311" src="https://github.com/user-attachments/assets/df33c842-1d77-4baf-b485-9512da6f4ce4" />

Despite using this picture for reference and trying to figure out how to route it properly, I was still unable to connect the traces. After taking a break from routing for a while, I came back and completely deleted
my traces to restart. This time, I used lots of vias on the diode tracks, switching it to the back layer everywhere I needed to run neopixel traces. This worked, as I was able to route my 
