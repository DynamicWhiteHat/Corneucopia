---
title: "Corneucopia"
author: "DynamicWhiteHat"
description: "A Corne Based 42 Key Mechanical Keyboard"
created_at: "2025-06-04"
---

# Total time spent: 10.25 hours

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

## Time Spent: 2.5 hours

## June 5: Restart using KiCad

Since I've made macropads and keyboards before in KiCad, making a schematic was relatively easy. I first started by selecting my MCU. I wanted the board to be wireless and have a display. Based on these parameters, I 
chose the Nice!Nano, since it comes from the same family as the Nice!View, and it supports wireless connectivity using ZMK. However, when buying the MCU, I will buy the Supermini NRF52840, which is a much cheaper
drop in replacement. I installed a popular keyboard library for KiCad called marbastlib and placed down the included Nice!Nano symbol.

Then, I added in the switches, which are chocs. I want this build to be low-profile, so chocs will fit this use case perfectly. I added 21 keys to each side, giving me a total of 42 keys. I also wanted to have per-key RGB,
so I added a neopixel for each switch. Then, I looked on typeractive.xyz for their power switches and found the JS102011CQN, an SPDT switch by C&K, as well as their reset button, which is manufactured by Panasonic. I imported these
symbols into my schematic and wired them up as well. Finally, I added a 2 pin JST connector for the battery and a 1x5 header for the OLED display. This is what my final schematic looks like:

<img width="1157" height="567" alt="image" src="https://github.com/user-attachments/assets/277a68a0-5d97-4113-bf9f-4fbfbf0bdf2e" />

## Time Spent: 1.5 hours

## June 6: PCB Work

I imported the PCB from the schematic, and I was blasted with various components. Although the schematic looked clean, the footprints from the marbastlib library had lots of drawings on them for placement, which made everythign
look larger than it actually was. I also imported the DXF outlines from Ergogen to help me with my key placement. I began placing the keys in their squares, which did require changing KiCad's rotation paramters, and once I was done, this is what it looked like:

<img width="1170" height="413" alt="Screenshot 2025-06-05 041530" src="https://github.com/user-attachments/assets/e9defc8c-f956-46b5-882e-54c9f5296239" />

Next, I placed the neopixels into their spots. The footprint for the switches had rectangles for where the neopixels should go, which made it easy to place.

<img width="480" height="455" alt="image" src="https://github.com/user-attachments/assets/5e036661-e152-4c2e-a1de-bc67d6231935" />

I placed the neopixels, once again using custom rotation paramters to fit the thunb cluster's rotation, and placed the last few remaining components as well. I also decided to add a rotary encoder to help it stand out as a fully custom keybaord.
This is what my fully layed out PCB looks like:
<img width="784" height="614" alt="Screenshot 2025-06-05 041536" src="https://github.com/user-attachments/assets/e823bf8e-a3a4-42e5-84d1-81310974e453" />
<img width="522" height="379" alt="Screenshot 2025-06-05 041541" src="https://github.com/user-attachments/assets/ecaf366b-9080-41ce-9004-dfd156c7286f" />

Next, I moved onto routing. First, I routed the diodes together, which was relatively simple. However, after this, routing became much more difficult. When I tried to route the neopixels, the traces for the diodes would come in the way.
No matter how many times I tried rerouting both the neopixels and the diodes, I was unable to figure out the correct way to route them. I decided to consult my previous keyboard design and follow that wiring. This was my previous wiring:
<img width="1493" height="341" alt="Screenshot 2025-06-06 114311" src="https://github.com/user-attachments/assets/df33c842-1d77-4baf-b485-9512da6f4ce4" />

Despite using this picture for reference and trying to figure out how to route it properly, I was still unable to connect the traces. After taking a break from routing for a while, I came back and completely deleted my traces to restart. This time, I used lots of vias on the diode tracks, switching it to the back layer everywhere I needed to run neopixel traces. This worked, as I was able to route my PCB switches. Next, I wired the encoder, jst connector, and the oled headers, which was relatively easy since they were on one side of the board. This is what my final PCB looks like:

<img width="1317" height="643" alt="image" src="https://github.com/user-attachments/assets/d7edf321-9284-4938-bcd1-57c380c865de" />

## Time spent: 3 hours

## July 20: CAD

Today I started the CAD. I began by importing the board outline DXF from Ergogen into Fusion and using the offset tool to make a wall of 1.8 mm.
<img width="1026" height="724" alt="image" src="https://github.com/user-attachments/assets/2f6291c6-9438-4506-aadf-8d554c08b673" />

I extruded this sketch to a total height of 12 mm, which gave it a good edge and enough clearance on the bottom. I also projected the circles from the m2 mounting points on my PCB onto a sketch and extruded them, which added mounting points to my case. This is what it looks like:

<img width="503" height="384" alt="image" src="https://github.com/user-attachments/assets/286b3720-94fd-4fc8-aa22-aedcdb455405" />

Then I used the DXF to make a plate of 2 mm to allow my switches to sit in them. The plate has no other mounting mechanisms, as it will rely on the connection of the swicthes to the plate. I had to cut out a rounded rectangle near the MCU since it sticks up, which took some time. I designed a sketch for this cutout:

<img width="355" height="601" alt="image" src="https://github.com/user-attachments/assets/624d0e72-7814-427e-bb2a-c2010ad2b330" />

Then I used the same sketch to create an acrylic piece to go over the OLED display. I saw it in [this](https://www.etsy.com/listing/1337908749/ready-to-use-crkbd-corne-keyboard-v301) listing, which I really liked. I also added some hexagonal threaded standoffs  to screw it in to my plate, but that's when I ran into an issue. I was unable to extrude the hexagonal standoffs onto the plate since the encoder was in the way. This is when I decided to drop the encoder alltogether. The whole time I was designing my PCB I was unsure if I should use the encoder, since it seemed like it was in an unnatural spot, so once I ran into this issue, I removed it from my PCB.

<img width="786" height="643" alt="image" src="https://github.com/user-attachments/assets/3b392a49-edd8-47de-8725-6a81891096a7" />


## Time spent: 2.5 hours

## July 31: Finish CAD

Today I finished the CAD. I started by adding in some rounded rectangles where the power switch and the reset button were. I used the point to point move tool to place it in the center of each component. To make it look nice, I also chamfered the edges. 

<img width="683" height="348" alt="image" src="https://github.com/user-attachments/assets/626478c0-39d2-44e3-ae37-91c45fc5574f" />

Then I shaped out a nice curve into the side of my case to make it look better. I initially attempted to use the loft and sweep tools, but I was unable to figure out how to work them. I instead opted to use the spline tool in a regular sketch and extruded that into the side of my case. I think this looks great:

<img width="318" height="301" alt="image" src="https://github.com/user-attachments/assets/85534e26-9590-498e-80d0-68abe4cc1666" />
<img width="336" height="242" alt="image" src="https://github.com/user-attachments/assets/8b0faf09-923a-4633-be70-3b7e0845a5ac" />

Next, I added in the USB C hole. I have made plenty of these before, so I did it quickly. I projected the existing shape of the USB C on the 3D model and added a 1.5 mm offset to allow the plastic housing around a USB C cable. I then extruded this sketch forwards through the case, then extruded the projection without the offset towards the USB C, finishing the hole. The final hole is visible above.

Finally, I mirrored the whole case design and each of its components to make the right half, since everything was placed in the same spot on both halves. My case is now finished. I took some renders and saved my final project.

![Corneucopia_OG_2025-Jul-31_08-42-40PM-000_CustomizedView587266445](https://github.com/user-attachments/assets/2f44400f-d4b5-4c38-b983-71c0e678fce8)
![Corneucopia_OG_2025-Jul-31_08-20-03PM-000_CustomizedView29841171726](https://github.com/user-attachments/assets/6ef8888b-e9b1-46a9-82fd-f04b0927b2ea)

## Time spent: 45 minutes
