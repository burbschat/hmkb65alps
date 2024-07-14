# HMKB 65 Alps Compatible PCB and Plate
## Case
* HMKB V1 65 AAA

## Layout
Raw data for [keyboard-layout-editor.com](http://www.keyboard-layout-editor.com):
```json
["~\n`","!\n1","@\n2","#\n3","$\n4","%\n5","^\n6","&\n7","*\n8","(\n9",")\n0","_\n-","+\n=",{w:2},"Backspace",{a:7},""],
[{a:4,w:1.5},"Tab","Q","W","E","R","T","Y","U","I","O","P","{\n[","}\n]",{w:1.5},"|\n\\",{a:7},""],
[{a:4,w:1.75},"Caps Lock","A","S","D","F","G","H","J","K","L",":\n;","\"\n'",{w:2.25},"Enter",{a:7},""],
[{a:4,w:2.25},"Shift","Z","X","C","V","B","N","M","<\n,",">\n.","?\n/",{w:1.75},"Shift",{a:7},"",""],
[{a:4,w:1.25},"Ctrl",{w:1.25},"Win",{w:1.25},"Alt",{a:7,w:6.25},"",{a:4},"Alt","Fn","Ctrl",{a:7},"","",""] 
```
Matrix position annotated version (also without label position information as this messes with scripts using the annotated version down the line):
```json
["0,0","0,1","0,2","0,3","0,4","0,5","0,6","0,7","0,8","0,9","0,10","0,11","0,12",{w:2},"0,13","0,14"],
[{w:1.5},"1,0","1,1","1,2","1,3","1,4","1,5","1,6","1,7","1,8","1,9","1,10","1,11","1,12",{w:1.5},"1,13","1,14"],
[{w:1.75},"2,0","2,1","2,2","2,3","2,4","2,5","2,6","2,7","2,8","2,9","2,10","2,11",{w:2.25},"2,13","2,14"],
[{w:2.25},"3,0","3,1","3,2","3,3","3,4","3,5","3,6","3,7","3,8","3,9","3,10",{w:1.75},"3,12","3,13","3,14"],
[{w:1.25},"4,0",{w:1.25},"4,1",{w:1.25},"4,2",{w:6.25},"4,5","4,9","4,10","4,11","4,12","4,13","4,14"]
```

Find in proper json format in `hmkb65alps.json`.
The corresponding **annotated** (i.e. which key goes where in the matrix) in
[kle-serial](https://github.com/ijprest/kle-serial) format can be found in
`hmkb65alps-annotated_kle-serial.json` (converted using
[this](https://adamws.github.io/kle-serial/)).

## PCB
### Ideas
* Consider using chips containing multiple diodes in the same package to avoid soldering pain
* Use Alps/MX hybrid footprints
* Consider Alps/MX hybrid plate
* Mill-Max Sockets for hot-swapping (should also work with hybrid footprints as seen in the pictures [here](https://blog.keeb.io/how-to-make-your-keyboard-hotswappable-with-mill-max-sockets/)).

### Footprints etc.
Included as submodules in `lib/`. 
* [ai03-2725's MX_V2](https://github.com/ai03-2725/MX_V2) for switch footprints
* [ai03-2725's Type-C.pretty](https://github.com/ai03-2725/Type-C.pretty) for USB-C port footprints
* [ai03-2725's random-keyboard-parts.pretty](https://github.com/ai03-2725/random-keyboard-parts.pretty) for USB-C port footprints
The MX_V2 (which also contain ALPS footprints) are fine, the other ones are not
quite to my taste.
Found a ALPS switch model [here](https://www.thingiverse.com/thing:3829342/files). 
Very kindly there is an scad file provided (and not just a mesh `.stl` or similar)!

#### 3D Models for Key Switches

### Components
#### USB-C Connector
All of the options here are selected to be hand solderable.

`Korean Hroparts Elec TYPE-C-31-M-12` Seems to be a popular choice, probably because it's dirt cheap (<20cents).
However, it's not available on DigiKey, Mouser or RS. 

`GCT` offers a series of hand solderable connectors.
[Compare them here](https://gct.co/product-compare/usb/usb4085,usb4105,usb4730,usb4800,usb4215).
Note that `USB4085` is entirely through hole, which however at the same time makes accessing the pins challenging.
For this PCB the accessible D+/D- pins were in the wrong order, which is why a different connector was used.
`USB4105` and `USB4215` seem to be essentially the same, with `USB4215` having some locating plastic pegs on the bottom.
The latter however seems not to be available at the usual vendors, so here `USB4105` is choosen as an slighly less cheap
alternative to the dirt cheep `HRO` mentioned above.
`GCT` also has very well structured documentation and links to footprints and 3d models on their website.


#### `kbplacer`
Used this [Kicad Plugin](https://github.com/adamws/kicad-kbplacer) for helping
with schematic/layout generation.
There is also a script `layout2schematic.py` in the repository which was used
to generate the key matrix part of the schematic.
Technically one can also access this when the `kbplacer` python package is
installed with `python -m layout2schematic`, but in this case the dependencies
will not be automatically synchronized. The best way probably is to use a
`hatch` virtual environment. Clone the repo and make sure `hatch` is installed.
The `pyproject.toml` defines a `hatch` virtual environment for the tools. To
create it run `hatch env create tools`. To launch a shell with the environment
activated use `hatch -e tools shell`. One may also just run this right away as
this will create the environment if not present.
Btw. for some reason from the `hatch` environment `pythom -m layout2schematic`
does not seem to work, so run the script from the `tools` directory directly.
See also the [the readme file for the tools](https://github.com/adamws/kicad-kbplacer/blob/master/tools/README.md) for more information.

Note that the input `json` file is not directly what is obtained from the [keyboard layout editor](http://www.keyboard-layout-editor.com)!
Use [https://adamws.github.io/kle-serial](https://adamws.github.io/kle-serial/)
or [keyboard-tools.xyz/kle-converter](http://keyboard-tools.xyz/kle-converter)
(as the main README file notes).
In any case, the layout file must be one where the keys in the keyboard layout
editor are annotated using labels as `row,col` to designate where they will be
in the matrix.
Find annotated layout in `hmkb65alps-annotated.json`

**TLDR**: 
```
cd kicad-kbplacer
hatch run tools:layout2schematic -in ../hmkb65alps-annotated-converted.json -out ../pcb/hmkb65alps-matrix.kicad_sch
```
Creates the base matrix schematic which I then manually edited to fit my
preferences.
I load this as a hierarchical sheet into the main kicad project.
~~As I prefer to not use global labels for the rows/columns, I also manually
replace the global labels with hierarchical labels.~~
**Bad idea as this breaks the net resolving with `kbplacer` it seems :(.**
So global labels it is (I also tried if local labels work, but they dont).
TLDR: Use the matrix as generated by `layout2schematic.py`, no touchy.

##### Generating the layout
If you do not do anything funny to the generated key matrix schematic (like
trying to use hierarchical labels), assigning footprints to all parts, then
importing to the pcb layout and running the plugin should just work.

I first assign 1U switches to all of the switches, have them placed and then
adjust the longer ones (way easier than trying to figure out which switch was
where in the matrix.)

When running the plugin point *Keyboard layout file* to
`../hmkb65alps-annotated-converted.json` (or wherever the layout in the correct
format is).
With the MX-Alps hybrid footprints the diode position must be adjusted, as
otherwise it is too close to the holes in the PCB which is not good to begin
with and also will cause the automatic routing to fail.
In *Switch diodes setting* set *Position* to *Custom*. I Chose *Offset X =
7.5*, *Offset Y = -6.5*, *Orientation = -90* and *Side = back*.

Probably better use the *Relative* mode. This will result in the layout for the
first switch being replicated to the others. For some reason this however does
not seem to work for open ended tracks.


##### Design Rules
Set approximately to what JLCPCB should be able to do withouth problems.


## Plate
### Design
[ai03 Plate Generator](https://kbplate.ai03.com/) seems to be a well made modern solution (repository [here](https://github.com/ai03-2725/yet-another-keyboard-builder))!
Probably prefer using this over [what used to be the standard tool(?)](http://builder.swillkb.com/) to get plate hole locations
(select no outline, as the correct one is not available there), then manually
add the correct outline from the MX plate files distributed on the HMKB
discord.

**Holdup**, on closer inspection `swillkb` seems to provide [much more features](http://builder-docs.swillkb.com/features/)!
In fact one can adjust the stabilizers for specific keys using special attributes in the layout definition.
This one for example overrides the spacebar stabilizer to be of Cherry + Costar type by using `{a:7,w:6.25, _s:1}`.
```
["~\n`","!\n1","@\n2","#\n3","$\n4","%\n5","^\n6","&\n7","*\n8","(\n9",")\n0","_\n-","+\n=",{w:2},"Backspace",{a:7},""],
[{a:4,w:1.5},"Tab","Q","W","E","R","T","Y","U","I","O","P","{\n[","}\n]",{w:1.5},"|\n\\",{a:7},""],
[{a:4,w:1.75},"Caps Lock","A","S","D","F","G","H","J","K","L",":\n;","\"\n'",{w:2.25},"Enter",{a:7},""],
[{a:4,w:2.25},"Shift","Z","X","C","V","B","N","M","<\n,",">\n.","?\n/",{w:1.75},"Shift",{a:7},"",""],
[{a:4,w:1.25},"Ctrl",{w:1.25},"Win",{w:1.25},"Alt",{a:7,w:6.25, _s:1},"",{a:4},"Alt","Fn","Ctrl",{a:7},"","",""]
```
This is exactly what I need for the Tai-Hao Keycaps which have cherry type stabilizers on only the spacebar.
Seems like one can also further [specify the outline](http://builder-docs.swillkb.com/features/#custom-polygons).
If possible, defining the whole plate programatically would be cool.
Actually, we could get away without using the web interface alltogether by using [`KAD`](https://github.com/swill/kad),
the library powering [builder.swillkb.com](http://builder.swillkb.com/).

**Holdup**, but `swillkb` does not do rounded corners as I might need for a PCB plate.
So I forked ai03 Plate Generator (aka yet-another-keyboard-builder) and 
[modified the code](https://github.com/burbschat/yet-another-keyboard-builder/tree/key_specific_overrides) 
with my essentially non existent javascript knowledge, which actually worked!
It's probably not pretty or good practice though, but good enough for what I need for now.

Here is the layout that should fit for stabiliziers for the Tai-Hao Alps keycaps:
```
["~\n`","!\n1","@\n2","#\n3","$\n4","%\n5","^\n6","&\n7","*\n8","(\n9",")\n0","_\n-","+\n=",{w:2},"Backspace",{a:7},""],
[{a:4,w:1.5},"Tab","Q","W","E","R","T","Y","U","I","O","P","{\n[","}\n]",{w:1.5},"|\n\\",{a:7},""],
[{a:4,w:1.75},"Caps Lock","A","S","D","F","G","H","J","K","L",":\n;","\"\n'",{w:2.25},"Enter",{a:7},""],
[{a:4,w:2.25},"Shift","Z","X","C","V","B","N","M","<\n,",">\n.","?\n/",{w:1.75},"Shift",{a:7},"",""],
[{a:4,w:1.25},"Ctrl",{w:1.25},"Win",{w:1.25},"Alt",{a:7,w:6.25, _s:"mx-basic"},"",{a:4},"Alt","Fn","Ctrl",{a:7},"","",""]
```

I also generated the plate with flipped Alps stabilizers as 
```
["~\n`","!\n1","@\n2","#\n3","$\n4","%\n5","^\n6","&\n7","*\n8","(\n9",")\n0","_\n-","+\n=",{w:2,_rs:180},"Backspace",{a:7},""],
[{a:4,w:1.5},"Tab","Q","W","E","R","T","Y","U","I","O","P","{\n[","}\n]",{w:1.5},"|\n\\",{a:7},""],
[{a:4,w:1.75,_rs:180},"Caps Lock","A","S","D","F","G","H","J","K","L",":\n;","\"\n'",{w:2.25,_rs:180},"Enter",{a:7},""],
[{a:4,w:2.25,_rs:180},"Shift","Z","X","C","V","B","N","M","<\n,",">\n.","?\n/",{w:1.75,_rs:180},"Shift",{a:7},"",""],
[{a:4,w:1.25},"Ctrl",{w:1.25},"Win",{w:1.25},"Alt",{a:7,w:6.25, _s:"mx-basic"},"",{a:4},"Alt","Fn","Ctrl",{a:7},"","",""]
```
and `alps-aek` instead of `mx-basic` for the spacebar which I then all composed in KiCad, which was possible
as the cutouts do not overlap.
This means that I do not have to worry about the orientation of the stabilizers (some Tai-Hao keycaps 
seem to have them inversed) and can later decide if I want alps or Cherry stabilizers on the spacebar 
(Tai-Hao keycaps support those on only the spacebar but there seem to also be adapters to use Alps stabilizers).


### Material
* Try lasercutting ~1.6mm plate on the lasercutter that is avaiable at my
university (even though it is not rated to cut metal this thick)
    * Have to source metal plates which might not be cheap in small quantities
* Order FR4 plate (i.e. just a PCB). This seems to be very reasonably priced.
Getting FR4 stock cheaper and cutting on the lasercutter appeared difficult
(could not find very cheap FR4 stock).
    * Ordering a PCB in plate size seems to cost around 3000JPY. One could also
    get an aluminum PCB for just a little more, but I don't know if an aluminum
    plate is a good idea. FR4 appeared much more sturdy to me but I did not
    make a direct comparison.

### Laser Cutting Services
* [sculpteo](https://www.sculpteo.com/)
* [ponoko](https://www.ponoko.com/)
* [株式会社かねよし](https://www.kaneyoshidesu.co.jp)
* [laserboost](https://www.laserboost.com/) seems reasonable but is based in Europe (Spain it seems) so shiping ends up expensive (~50 Euros)

## References
### PCB Design
[Masterzen's blog](https://www.masterzen.fr/2020/05/03/designing-a-keyboard-part-1/) (multiple parts)
