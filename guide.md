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
