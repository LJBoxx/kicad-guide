# Kicad starter guide

So you want to make a circuit board, but dont know where to start ? 

Dont worry i gotchu. Here you will learn how to use the basics of kicad, and I'll give you some tips I learned making pcbs for the last few years. 

## Basics
So first things off, install kicad, and draft out what you want your project to look like. In my case i will make a pcb card with few leds and an nfc tag :)

After that, head to github to make your repo, name it and give it a kicad gitingore (so u dont push out the lock files that can be annoying and also history since it will be tracked by your push history/lapse :p) 

Choose a licence to your wishes too, MIT license is good.
![alt text](image-1.png)

Then you can clone your repo on your computer if you use cli, you know what ur doing already :)
Else if you are lazy like me and use github desktop just add the repo or you could even create it there
![alt text](image-2.png)

### Opening kicad for the first time.
![alt text](main.png)
okay that might look scary.... Though its not even the scariest ;-;

So first as you can see below ```[no project loaded]``` you have to create a new project (click on new project !)

![alt text](image.png)

In kicad 10, they have introduced templates, we wont be using it here and for most simple projects. Select default and it will prompt you to select a directory.

![alt text](image-3.png)

Name your project how you want it, it's not that relevant 

![alt text](image-4.png)

Once that's done, you will have a (project name).kicad_pcb and kicad_sch, these files contains the data of your pcb and your schematic.

![alt text](image-5.png)

Now open the kicad_sch file that will be where you define how each component is wired to the others.

![alt text](image-6.png)

Okay now that is scarier than before but dont worry I'll break down the only parts you need.

To place components you have to use this tool (or press a):
![alt text](image-7.png)

You can type out what components you need, for me I will use some LEDs 

![alt text](image-8.png)

Here is my led !

![alt text](image-9.png)

Once you press okay it will drag it and you can place it anywhere on the sheet.

![alt text](image-10.png)

Okay that's nice I have an led on my sheet but now what else do i need ...? SOME POWERRRR!!! For this you can use the Power symbol tool (p) on the toolbar just under place symbol tool 

![alt text](image-11.png)

Same thing as for parts drag and drop. I needed ground and Vcc (which means + voltage and vss is the same but for ground) 

![alt text](image-20.png)

To wire parts together, use the wire tool (w) or press on the small round dot on the pin.

![alt text](image-18.png)
![alt text](image-19.png)

Once wired it looks like this and remember grounds point down and voltage points up.

![alt text](image-12.png)

Great now i have an led and I have defined where power and ground goes. Now i need to *actually* give it power either by wiring a battery or in my case i will have nfc on my card and there is an nfc chip that has an "energy harvest" output pin meaning I can get power from the nfc field that powers the chip !! The ic is the NT3H2111 from NXP semi

![alt text](image-13.png)

To find this part i will head to [LCSC](https://www.lcsc.com) and type the part reference to see what they have in stock. Also why lcsc you may ask ? Well they are usually the cheapest, and parts available on lcsc are also usually available for assembly by jlcpcb though in that case you want to use basic parts so that you wont have to pay the 3$/ part that's not a basic one in [their part library](https://jlcpcb.com/parts/in-stock-parts)

![alt text](image-14.png)

Bingo ! they have 3 packages in stock but if i look for the part in kicad... Well i cannot find it. that's why i will use [easyeda2kicad](https://github.com/uPesy/easyeda2kicad.py) in order to retrieve the part from easyeda (another editor but with jlc's library) and transfer it over to kicad. You should follow the instructions in the repo for installation.

I have a hot air station at home which means I can solder the very small package but you should try to use the biggest one available since it will be wayy easier to solder. In this case you would pick the SO-8 package with the lcsc id C2654859

The annoying part is actually figuring out how this chip work and I'd recommend going through the datasheet thoroughly and actually listing what you need. If the chip does not match what you need feel free to search for another chip. I'm actually in luck here because they provide an example schamtic :)

![alt text](image-17.png)

Now getting the part into kicad, the 3d model wasn't available. It's okay, we can fix it later and find a model afterwards
![alt text](image-15.png)

Here it is in kicad.

![alt text](image-16.png)

Okay so we know that vout will be between 2.2 and 3v and it need a capacitor of 150 to 200nf. We can now proceed to wire the antenna, led and capacitors. We wont limit the current going to the leds with a resistor (which if powered from a battery you would want to) because the supply is limited at 15ma max. I will add 3 more leds in parallel :)

By the way for any pins you dont use you should flag it with this tool (q) :

![alt text](image-25.png)

![alt text](image-22.png)

As for the capacitor and resistor it is the same symbol. You can edit the fields containing its value to whatever one you need. Here i have added an unpolarized capacitor and double click on the "C" to edit it. For resistor value you would put 5r for 5ohm and 5k1 for 5.1kilo ohm. You can put anything its just easier to read. As for capacitors its the same 5f for 5 farad (who uses that much capacitance wow) and 5n for 5 nanofarad / 5u for 5 microfarad and so on. Check out the [RKM](https://en.wikipedia.org/wiki/RKM_code#Part_value_code) wiki page !

![alt text](image-23.png)
![alt text](image-24.png)

Alright my schematic is done here. I will now run the ERC (Electrical Rules Checker) to see if everything is wired correctly. 

![alt text](image-26.png)

Oh wow okay so ERC checks for how the pins are configured and well the symbol imported from easyeda didnt have them. It's not always necessary to fix them but as you get to more and more complex projects its good practice to do so in order to catch any mistakes (wrong wire input going into input and other stuff like so). So to fix these errors you will have to select the symbol and right click then properties (or just select and press e). If you dont understand anything in this part its fine. 

![alt text](image-27.png)

Okay now you have this window that opens. Press on "edit symbol" as we want to edit it.

![alt text](image-28.png)

Yep they are "unspecified".

![alt text](image-30.png)

Double click on one of them to edit it.

![alt text](image-31.png)

