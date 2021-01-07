
```
elf.moveTo(lollipop[1])
elf.moveTo(munchkin[0])
ques = elf.ask_munch(0)
elf.tell_munch(ques.filter(elem => parseInt(elem) == elem))
elf.moveUp(10)



for (i = 0; i < 4; i++)
elf.moveTo(lollipop[i])

elf.moveTo(lever[0])
elf.moveDown(6)
elf.moveTo(munchkin[0])
ques = elf.ask_munch(0)
keys = Object.keys(ques)
for (i = 0; i < keys.length; i++) {
  if (ques[keys[i]] == "lollipop") {
    elf.tell_munch(keys[i])
    elf.moveUp(10)
  }
}
```
