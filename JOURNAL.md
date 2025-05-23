---
title: "DoNotDelta"
author: "Parker Rupe"
description: "This is a first-of-its-kind hybrid delta/quantum delta 3d printer."
created_at: "2025-05-21"
---
This is my journal of the design and building process of the DoNotDelta. 


### 5/21/2025 - 4 hours spent

![image](https://github.com/user-attachments/assets/c7ef615b-b4a7-46b6-9300-a9e6aeef7fd7)

Today was the beginning of design. First things first, I made the bottom base, with the printed frame, bottom panel, and motor assemblies, which contain pulleys and bearings. 

![image](https://github.com/user-attachments/assets/2b97b8d0-0c39-402f-a339-ae0fe06e48a3)

The bottom bases consist of an ABS print and a carbon fiber panel. These carbon fiber panels may end up being printed, depending on the cost for manufacture. I also designed the double shear modules to slide into the main base and then be bolted in. 
![image](https://github.com/user-attachments/assets/6ff311aa-fe11-45fc-a861-29fc10288f12) ![image](https://github.com/user-attachments/assets/1d65cb17-80e9-425a-a386-89898113a541) 

Double shear is in essence supporting the end of the motor shaft with a bearing. This puts the shaft in two shear planes rather than one. This means that when I properly tension the belts it won't do any harm to the motor 
shafts or motor bearings. 
Then, I mirrored that vertically and added in 10mm linear rods. 

![image](https://github.com/user-attachments/assets/42f2b44b-d235-4189-ae56-6d2460be4059)

I chose 10mm linear rods rather than your typical 6 or 8 as the linear rods are structurally important. They do not add much to the price. 


After that, I decided to add electronics mounting/frame stabilization via din rails. 
![image](https://github.com/user-attachments/assets/2efdec88-a63b-479d-b94a-403c42209909) 

These are a very useful electronics mounting standard, and will also add rigidity to the printer. 
The frame is now completed. 


I quickly moved on to designing the carriages. They needed to house linear bearings, a belt tensioning method, and mounting for the effector arms. 

![image](https://github.com/user-attachments/assets/b39f4c5a-67f4-476b-ae00-bd9615a8eb57) ![image](https://github.com/user-attachments/assets/f05552bb-06b1-4de5-8174-929307d2bf4d)

The blue square pictured is the belt tensioning setup, which clamps onto the belt using a wedge system and then is tightened via a screw on top. These are designed so that the belt will snap before the tensioner comes loose. 

I copied that 6 times, and the carriages were now figured out.

![image](https://github.com/user-attachments/assets/edc7b14b-4236-459a-9cc6-e972ed915bac)

Lastly for this session, I calculated an estimate for the delta arm lengths and modeled those in. I used the equations found here: https://reprap.org/wiki/Delta_geometry#Schematics

![image](https://github.com/user-attachments/assets/bafed811-a702-4ed7-941d-cf7011b07166)

All that is left is to do is the two effectors (think: toolhead and bed), the belt idlers, and finishing touches (like screws and electronics). 

![image](https://github.com/user-attachments/assets/9355e801-524a-46f6-9dcc-685c8a8ce343)




### 5/23/2025 - 6 hours spent

![image](https://github.com/user-attachments/assets/d8960fa1-78cd-4d5a-8cae-d90866830a07)

Today I tackled the effectors and extruder. I adjust the arm length to fit better with the bearing rod ends I am using and designed the effector itself. I am using a bambulabs p1 hotend clone, as it's decent flow for 8 bucks. I did not add part cooling - I am unsure if I will have any. If I do, it will be utilizing compressed air. 

![image](https://github.com/user-attachments/assets/bf8950d3-7d5c-4b07-bcec-367a0e1d80d2)

I duplicated the base effector to the top. I will be using the effector itself as the print bed in this first revision. Later on it may become heated and made out of CF plate, but for now it will be abs with painters tape on it. Lightweight and dirt cheap. 

I optimised the arm length using a wonderful delta analysis tool from my friend Deadlock. https://github.com/dead-lock-ed/DeltaCalcs. Wonderful tool. This gave me 76.5mm arm length. A good balance between accuracy (max of 0.022mm variance) and not too much of a speed reduction at the edges (2.5). 


![image](https://github.com/user-attachments/assets/b8811687-dabe-4950-bb10-bb2b61c012a8)

This is what the whole printer now looks like. I moved the din rails to the sides of the towers so that they can later on be used to support the idlers. It also doesn't block the view this way. 


![image](https://github.com/user-attachments/assets/b03337ee-39cf-4953-a6ea-91837e7f8d9b)

Lastly, I added the boombox extruder by Colphaer. This is the best bowden extruder on the market, using two full size nema 17s to move the filament. Ideally I would pair it with a kevlar sheath around the bowden tube, but that is very expensive, so it will be added later. The reason for the kevlar sheath is that one of the biggest issues with bowden is the fact that the tube can move with the filament. So when filament is extruded, the tube gets pushed out, effectively ruining pressure advance. A tensioned kevlar sheath prevents the tubing from moving. Eventually, I will add this. 

This was all for today. It wasn't nearly as much progress as the last entry, but now you can actually tell it is a 3d printer. 
