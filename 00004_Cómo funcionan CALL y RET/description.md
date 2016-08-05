
```
rutA: MOV R3, 0x005F 
      ADD R3, R1
      MUL R3, 0x0012 
      RET
```
```
rutB: ADD R2, 0x0100 
      DIV R4, R2
      RET
```
Y luego se ensamblan de la siguiente manera:
```
CALL rutA
CALL rutB
```