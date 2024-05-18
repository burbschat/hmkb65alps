# HMKB 65 Alps Compatible PCB and Plate
## Case
* HMKB V1 65 AAA

## Layout
```json
["~\n`","!\n1","@\n2","#\n3","$\n4","%\n5","^\n6","&\n7","*\n8","(\n9",")\n0","_\n-","+\n=",{w:2},"Backspace",{a:7},""],
[{a:4,w:1.5},"Tab","Q","W","E","R","T","Y","U","I","O","P","{\n[","}\n]",{w:1.5},"|\n\\",{a:7},""],
[{a:4,w:1.75},"Caps Lock","A","S","D","F","G","H","J","K","L",":\n;","\"\n'",{w:2.25},"Enter",{a:7},""],
[{a:4,w:2.25},"Shift","Z","X","C","V","B","N","M","<\n,",">\n.","?\n/",{w:1.75},"Shift",{a:7},"",""],
[{a:4,w:1.25},"Ctrl",{w:1.25},"Win",{w:1.25},"Alt",{a:7,w:6.25},"",{a:4},"Alt","Fn","Ctrl",{a:7},"","",""] 
```

## PCB
### Ideas
* Consider using chips containing multiple diodes in the same package to avoid soldering pain
* Use Alps/MX hybrid footprints
* Consider Alps/MX hybrid plate

## Plate
### Design
Use [this tool](http://builder.swillkb.com/) to get plate hole locations
(select no outline, as the correct one is not available there), then manually
add the correct outline from the MX plate files distributed on the HMKB
discord.

### Laser Cutting Services
* [sculpteo](https://www.sculpteo.com/)
* [ponoko](https://www.ponoko.com/)
* [株式会社かねよし]https://www.kaneyoshidesu.co.jp


## References
### PCB Design
[Masterzen's blog](https://www.masterzen.fr/2020/05/03/designing-a-keyboard-part-1/) (multiple parts)
