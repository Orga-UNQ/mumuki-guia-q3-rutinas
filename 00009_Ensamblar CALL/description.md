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

Un ejemplo de uso: `CALL rutA`

### Quién es el operando Origen?

Al respetar la ortogonalidad de la arquitectura Q, la instucción CALL puede estar acompañada por un operando en cualquier modo de direccionamiento. Es decir:

* Modo directo
* Modo inmediato
* Modo registro

Te imaginás como escribir una instrucción CALL en cada caso? Sería algo como lo que sigue:

|modo|ejemplo|
|----|-------|
|directo   | CALL [0xAABB]|
|inmediato | CALL 0xAABB|
|registro  | CALL R5 |


Interesante! Pero... a cual corresponde algo como `CALL etiqueta`?

## Hora de pensar

Supongamos que tenemos la siguiente rutina ensamblada a partir de la celda `3344`:

```
miRutina: SUB R6, 0xAAAA
          RET
```

> ¿Cómo es el código máquina de la instrucción `CALL miRutina`?
