# Novedades en Q3

La arquitectura Q3 especifica dos nuevas instrucciones: `CALL` y `RET`. `CALL` es la única instrucción de un operando orígen, y el formato de instrucción es

| codop | relleno | Modo Origen | Operando Origen|
|-------|---------|-------------|----------------|
| 4b    | 000000  |   6b        | 16 b           |

La tabla de códigos de operaciones es:

| Instrucción | codop | Efecto|
|-------------|-------|-----------|
| CALL        | 1011  | `PC<--Origen` |


¿Porqué se considera un operando Origen? Pues el nuevo valor de PC es, justamente, el operando, y el operando destino de la instrucción CALL es siempre el mismo: **el registro PC**


## Hora de pensar

Supongamos que tenemos la siguiente rutina ensamblada a partir de la celda `3344`:

```
miRutina: SUB R6, 0xAAAA
          RET
```

> ¿Cómo es el código máquina de la instrucción `CALL miRutina`?
