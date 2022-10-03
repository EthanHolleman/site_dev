---
title: "Print TPU without a direct drive extruder"
date: 2022-03-08
tags: ['3D Printing', 'blogs']
draft: false
---


These recommendations are in addition to general 3D printing best practices, namely
proper bed leveling and cleaning. Without a clean and level bed, none of this
advice will do you any good.

### 1. Print a filament guide; preferably one that uses a bearing for your printer

![](/posts/images/filamentGuide.png)


I print on an Ender3 and use [this guide](https://www.thingiverse.com/thing:4683505)
by [Mark Villela](https://www.thingiverse.com/markacho/designs). A filament
guide is an abosulte requirement to reduce the angle the filament must enter
the extruder gear at. Without one, the tension on the filament at the extruder
will be to great for it to push filament into the hot end.

### 2. Adjust slicer settings 

The default settings for generic TPU 95A in Cura were not conservative enough
to produce consistent prints. You need to print **slow**, **hot** and 
**without retractions**.

You can download my Cura TPU profile 
[at this link](/posts/data/EtH-TPU-Cura-Profile.curaprofile). If Cura is not your
preferred slicer a summary of the settings I changed are
shown below.

```
adhesion_type = skirt
material_bed_temperature_layer_0 = 70
alternate_extra_perimeter = True
material_print_temperature_layer_0 = 228.0
retraction_enable = False
speed_layer_0 = 10
speed_print = 20.0
```

### 3. Clean your nozzle

The stringy nature of TPU can cause it to stick to your printer's nozzle. If
there is a significant amount of TPU present on the nozzle before the print
begins, this can cause a spiral of extruded filament buildup on the nozzle
instead of the print bed. Clean the nozzle before starting or if its too far
gone just save yourself some time and replace it with a cheap brass 0.4 mm.


### 4. Print models one at a time

I have found that when you disable retractions you can get a lot of stringing between
objects. This is greatly reduced when you keep your prints to one main
object or print objects serially instead of all-at-once.