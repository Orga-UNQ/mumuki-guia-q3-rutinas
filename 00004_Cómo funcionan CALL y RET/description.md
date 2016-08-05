
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
```
CALL rutA
CALL rutB
```

La pregunta que nos hacemos es: ¿En que orden se ejecutan las instrucciones?

|Instrucción|Efecto|
|-----------|-----------|
|`CALL rutA`| DEsvía el flujo hacia la primer instrucción de la rutina A|
|``||
