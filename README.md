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

Find in proper json format in `hmkb64alps.json`.
The corresponding **annotated** (i.e. which key goes where in the matrix) in
[kle-serial](https://github.com/ijprest/kle-serial) format can be found in
`hmkb64alps-annotated_kle-serial.json` (converted using
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

## Plate
### Design
[ai03 Plate Generator](https://kbplate.ai03.com/) seems to be a well made modern solution (repository [here](https://github.com/ai03-2725/yet-another-keyboard-builder))!
Probably prefer using this over [what used to be the standard tool(?)](http://builder.swillkb.com/) to get plate hole locations
(select no outline, as the correct one is not available there), then manually
add the correct outline from the MX plate files distributed on the HMKB
discord.

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
Find annotated layout in `hmkb64alps-annotated.json`

**TLDR**: 
```
cd kicad-kbplacer
hatch run tools:layout2schematic -in ../hmkb64alps-annotated-converted.json -out ../pcb/hmkb64alps-matrix.kicad_sch
```
Creates the base matrix schematic which I then manually edited to fit my
preferences.
I load this as a hierarchical sheet into the main kicad project.
As I prefer to not use global labels for the rows/columns, I also manually
replace the global labels with hierarchical labels.

### Laser Cutting Services
* [sculpteo](https://www.sculpteo.com/)
* [ponoko](https://www.ponoko.com/)
* [株式会社かねよし]https://www.kaneyoshidesu.co.jp

## References
### PCB Design
[Masterzen's blog](https://www.masterzen.fr/2020/05/03/designing-a-keyboard-part-1/) (multiple parts)
