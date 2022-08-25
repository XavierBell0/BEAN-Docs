# REPAIRS

So, something broke? L. At least you have this repo of all the 3D printed parts of BEAN. The given parts are in STL form. If you need them as SLDPRT to make changes, go to the ASSEM folder. If you need them as 3MF or STEP files, export them from Solidworks as whatever file type you want. 

### Print settings
#### Printer
These aren't very large or very complicated prints. I would avoid SLA printing. It is a pain to wash and cure, and the parts will be weaker. SLA is only good if you need very precise parts with low tolerance. In our case, almost all FDM hobby printers will do. I used the Prusa i3 MK3, but you will also be fine on an Ender 3 or whatever you have. Just make sure the bed is level and you follow the basic guidelines of 3D printing (found everywhere online). Use Cura or PrusaSlicer.
#### Material
PLA is the easiest and most common 3D printing material. It prints reliably, is cheap, and is relatively durable. You probably won't need anything more expensive.
#### Supports
The hardest part of 3D printing is removing the supports. It is especially difficult on the gondola frame. In the slicer, use low density or far spaced supports. Flush angle cutters are your best friend. Detach the bottom first and work upwards in small chunks. Always cut off as opposed to tearing off. Be very gentle or else the beams will snap.
#### Press fits
The tolerance required for press fits will be different depending on your printer of choice. There is never a true 1:1 fit between CAD and 3D printing. First print one of the hole tests. Hole tolerances will be different if the hole is printing vertically vs horizontally. Print the vertical and horizontal fits for the motors. This is absolutely a pain to do, but trying to file the hole out is never faster. Cura has a setting for horizontal expansion, so if you have that dialed in correctly, the 1:1 CAD to reality will be closer.
