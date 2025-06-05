---
title: "DoNotDelta"
author: "Turtle"
description: "This is a first-of-its-kind hybrid delta/quantum delta 3d printer."
created_at: "2025-05-21"
---
This is my journal of the design and building process of the DoNotDelta. 
50 logged hours total

### 5/21/2025 - 5 hours spent

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




### 5/23/2025 - 8 hours spent

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


### 5/24/2025 - 12 hours spent

![image](https://github.com/user-attachments/assets/f0d330f5-eaad-42e6-9f92-a347d3078e90)

Today was a long one. Well, 2 days. Overnighter. But, the printer is finished save for part cooling. Which, technically, is optional. I'll take a look at what I have and what budget is looking like. But the next step is a detailed BOM and then submission!

So, first, I made the idlers. 

![image](https://github.com/user-attachments/assets/202d9099-cb9b-4152-b46a-1c33bb4bca22)

These are fairly simple. Two dead shaft idlers stacked vertically using 3mm screws as the dead shaft. This is also where I am housing the endstop switches. The smart move would be to put them at the very bottom and top of the printer, but I think it would look way cooler to have each delta gantry move one-at-a-time to the center and then back down. 
Because my tensioners are in the carriages, it makes the idlers very easy.

Also, while doing the idlers, I switched the pulleys and idlers to 16 tooth instead of 20 tooth, and the stepper motors from 1.8 degree to 0.9 degree.  I did this because after using the design tools I mentioned yesterday from Deadlock, I learned that 20 tooth idlers/1.8 degree steppers added an unnaceptable amount of potential locational deviance. The original setup was giving a total max deviance of 0.044mm, or 0.022 per side. This is not very good. With a 16 tooth/0.9 degree setup, I effectively halve that deviance, giving 0.011mm per side or 0.022mm total. These numbers are rounded, of course. This change actually affects the design very little, and saves money!

![image](https://github.com/user-attachments/assets/836debcb-9e9a-4bbe-8017-d5cb1b924815)

Next, I realized I possessed 3 extrusions of 330mm length. The exact size I need! So, I decided to replace the DIN rails with 2040 extrusions. These brace off the top/bottom plates, the printed frames, and the idler stacks. This will add so much rigidity to the printer, significantly increasing the potential maximum acceleration. And, once again, saves money. 

![image](https://github.com/user-attachments/assets/f22cd195-6e5e-472e-a21f-9061a9016809)

I then added the electronics and their respective mounting. I need a power supply, a mainboard, a screen, and an AC fused inlet. All of these were pretty quick to add and either mount on the 2040 extrusions or the printed frame. I chose not to add an electronics enclosure as that would make the printer harder to move. In exchange, I plan on doing NASA spec cable lacing using twine and color-coded wiring. It will be gorgeous - you will see. 

![image](https://github.com/user-attachments/assets/8d4fc891-3c46-4045-854f-8f6fe8c2bf7d)


![image](https://github.com/user-attachments/assets/244744cc-c329-4279-9447-f17c46805336)

________________________________________________________________________________________________

![image](https://github.com/user-attachments/assets/ff28ef16-5c2b-402b-8f51-408f7e7ca605)

Last, but certainly not least, I added all the screws. You can see them dotted everywhere - there is, well, a lot. 

The printer is physically finished with everything needed (and some extra of course). I still need to determine the applicability of part cooling and what I can afford. Then, it's a detailed bom, and firmware! I will probably try to order parts before firmware development, as they will take 2-3 weeks to arrive. 


### 5/25/2025 (night) - 8 hours spent 

![image](https://github.com/user-attachments/assets/047ef7ba-4056-4285-bbb8-178217cec5a0)

So, today was not actually all that much progress. I swapped the arm joints, made the arms round, and designed part cooling. The arms took an hour. Part cooling took 6. Ouch.
These are the joints I am now using. They are m3/3 7mm diameter mp-jet joints. Unfortunately, I could not find any existing designs of this part, so I had to recreate it by hand using provided drawings and a list of dimensions - found here https://mpjet.com/shop/img/cms/EN_KuloveCepyPg.png

![image](https://github.com/user-attachments/assets/fa095a2e-fda7-44e1-8749-65157233d441)

And then there was the part cooling. I am using either a deconstructed air duster or a roborock vacuum blower fan as remote cooling via a tube. Whichever fits in budget. I learned all the duct info from a wonderful video by James Pray. https://youtu.be/YijwkQCOBEA?si=hlhMq9mIeUlOrpgG
Basically, the flexible tube goes from the fan to the toolhead, and then passes through a splitter and gets routed through the delta effector plate via curved geometry inside of the hotend mount. Quite an elegant solution in my opinion, and it's lightweight. While I was at it, I redesigned the entire hotend mount to be lighter and stiffer. No more turtle vent. 

![image](https://github.com/user-attachments/assets/d404eadd-6301-4399-b97c-a055b74e5b23)

![image](https://github.com/user-attachments/assets/7b225bec-e08c-44ef-bc18-163404956f2f)

![image](https://github.com/user-attachments/assets/30eb7474-0df6-4012-a012-b480605228a4)

So yeah. That took 7 hours straight of design. But!! The printer is now completely done design wise - unless budget allows for a better screen. Overall, I am very happy with this design and will be submitting it shortly. 

![image](https://github.com/user-attachments/assets/a41d3409-154d-444c-b153-6401c276145f)


### 5/25/2025 (day) - 5 hours spent

Today was final touches. I adjusted the carbon fiber top and bottom plates to be stronger/cheaper to manufacture, added all the hardware, and last minute decided to design a small heated bed for the printer, which is also made of carbon fiber. I will be using a 15w 24v silicone heater. Super cheap but will get the job done. Overall, very, very happy with this design. 

![image](https://github.com/user-attachments/assets/bd60b481-2ab4-4163-ab0c-5f99cbac9858)

![image](https://github.com/user-attachments/assets/e6e8d90f-5193-4324-9324-b5ceec43e5aa)

![image](https://github.com/user-attachments/assets/02793e6e-21ce-4852-b18d-76866fc9649b)

![image](https://github.com/user-attachments/assets/6f42e468-97d6-433e-b018-75c289465d37)

Now, to write a bom and submit. 

### 5/27/2025 - 7 hours spent

Today was the last day of design and bom making. I went through my whole budget and realized I have enough left for a better hotend. And, remote hotend heatsink cooling using an aquarium pump. I spent about 4 hours designing the new toolhead and then the remaining 3 were spent on bom making. Also, after getting quotes from SCS and cncmadness, I decided to change all of my cut panels (bed, top/bottom, hotend mount) to 5052 aluminum. It is much cheaper. It is time to submit 

![image](https://github.com/user-attachments/assets/5ed22c0f-e467-4653-8099-2829492e094f)

![image](https://github.com/user-attachments/assets/7e715154-883f-4165-991f-5fa220ed4da6)

![image](https://github.com/user-attachments/assets/dd3050ca-aaf1-4a27-99e3-b09607d25611)


### 5/27/2025 - day time - 5 hours spent

I decided that my repo deserves some proper renders. So, I spent about 3 hours coloring everything as accurate as I can and then an hour playing with render settings and editing photos. You can see the results on the front page of this repo! 
Worth it!


### 6/4/2025 - 2 hours spent

Today marks the day that all orders have been placed. Plus, I moved the endstop positions. Having them at the middle, while looking cooler, is asking for a collision. So, I have to move the endstops to the top/bottom. It does make things a tiny bit more complex but thats okay. I may end up changing these to optical end stops for repeatability. Depends on what parts I have. Overall, it was very productive, and being on the call was cool. 

![image](https://github.com/user-attachments/assets/f08442e3-6df6-456d-8b93-b3c1e89e150c)
