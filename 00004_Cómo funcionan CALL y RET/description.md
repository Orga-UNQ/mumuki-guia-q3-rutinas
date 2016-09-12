Retomemos el ejercicio anterior. Teníamos el siguiente código:

```
rutA: MOV R3, 0x005F 
      ADD R3, R1
      MUL R3, 0x0012 
      RET
```
```
rutB: ADD R2, 0x0100 
      MOV R4, 0x0001
      DIV R4, R2
      RET
```
```
CALL rutA
CALL rutB
```

La pregunta que nos hacemos es: ¿En que orden se ejecutan las instrucciones? Para responderla, supongamos el siguiente estado inicial:

| variable | valor inicial|
|---------|-------|
| R1 | 0x0000 |
| R2 | 0x0001 |

Entonces se ejecuta la siguiente secuencia:

| |Instrucción|Efecto|
|---|-----------|-----------|
| 1 |`CALL rutA`| **Desvía el flujo hacia la primer instrucción de la rutina A**|
| 2 |`MOV R3, 0x005F`| R3=0x005F|
| 3 |`ADD R3, R1`| R3=0x005F+0x0000|
| 4 |`MUL R3, 0x0012`| R3=(0x005F+R1)*0x0012|
| 5 |`RET`| **Retorna el flujo al *programa principal* (la sig. instruccion)**|
| 6 |`CALL rutB`| **Desvía el flujo hacia la primer instrucción de la rutina B**|
| 7 |`ADD R2, 0x0100`| R2=0x0001+0x0100|
| 8 |`MOV R4, 0x0001`| R4=0x0001|
| 9 |`DIV R4, R2`| R4=1/(0x0101)|
|10 |`RET`| **Retorna el flujo al *programa principal***|

Otra pregunta que deberías estar haciéndote: ¿Cómo sabemos que la ejecución empieza en el primer CALL? Esa cuestión la retomaremos mas adelante...

#### Poner en práctica

Supongamos el siguiente código:

```
r2: MOV R1, 0x0000
    RET
r1: CALL r2
    RET
CALL r2
CALL r1
```

y supongamos que construimos una tabla de seguimiento como la de arriba:

|   |Instrucción|Efecto|
|---|-----------|-----------|
| 1 |`CALL r2`  | **Desvía el flujo hacia la primer instrucción de la rutina r2**|
| 2 |`MOV R1, 0x0000`| R1=0x0000 |
| 3 |`RET`| **Retorna el flujo a ??**|
| 4 | ?? ||


¿Cual es la siguiente instrucción a ejecutar?
