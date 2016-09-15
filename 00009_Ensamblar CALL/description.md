## El código máquina del CALL

La instrucción `CALL` es la única de un operando orígen, y el formato de instrucción es (ver [especificación](http://orga-unq.mumuki.io/exercises/2711-ejecucion-de-programas-q3-rutinas-especificacion-de-q3))


<table class="tg">
  <tr>
    <th class="tg-7geq">codop</th>
    <th class="tg-7geq">Relleno<br></th>
    <th class="tg-7geq">modo Origen<br></th>
    <th class="tg-7geq">operando Origen<br></th>
  </tr>
  <tr>
    <td class="tg-quxf">4 bits<br></td>
    <td class="tg-quxf">000000<br></td>
    <td class="tg-quxf">6 bits<br></td>
    <td class="tg-quxf">16 bits</td>
  </tr>
</table>

Como se indica en la  [especificación](http://orga-unq.mumuki.io/exercises/2711-ejecucion-de-programas-q3-rutinas-especificacion-de-q3), el efecto que se espera es: 

```
[SP]=PC; 
SP=SP-1; 
PC=Origen
```

**¿Porqué se considera un operando Origen?**

Pues porque el nuevo valor de PC es, justamente, el operando, y el operando destino de la instrucción CALL es siempre el mismo: **el registro PC**

Un ejemplo de uso: `CALL rutA`

### Quién es el operando Origen?

Al respetar la [ortogonalidad](https://en.wikipedia.org/wiki/Orthogonality_(programming)) de la arquitectura Q, la instucción CALL puede estar acompañada por un operando en cualquier modo de direccionamiento. Es decir:

* Modo directo
* Modo inmediato
* Modo registro

¿Te imaginás como escribir una instrucción CALL en cada caso? Sería algo como lo que sigue:

|modo|ejemplo|
|----|-------|
|directo   | CALL [0xAABB]|
|inmediato | CALL 0xAABB|
|registro  | CALL R5 |


Interesante! Pero... a cual corresponde algo como `CALL etiqueta`?

## Ensamblar una etiqueta

La etiqueta es un recurso muy práctico para los programadores, pero se pierden a la hora de ensamblar el código fuente en código máquina, convirtiéndose en las **direcciones reales** del codigo máquina de cada rutina.

Es decir, al ubicarse una rutina en memoria, se puede determinar **cuanto vale una etiqueta** y este valor es usado en todos los `CALL` que hacen referencia a la misma.

Por ejemplo, el siguiente código fuente está ensamblado a partir de `A000`

```
etiq: ADD R0, R1 
      RET
      
CALL etiq
```
Esto es equivalente a reemplazar:

```
ADD R0, R1 
RET
      
CALL 0xA000
```

Este criterio se basa en el efecto (o ejecución del CALL) que dice: `PC<- Origen`. Entonces, una vez ensamblada y ubicada en memoria, la dirección de inicio de la rutina no cambia, es constante o equivalentemente es de tipo **inmediato**

Veámoslo en un *mapa de memoria*:

|dir|contenido|corresponde a|
|---|---------|-------------|
|A000| 0010 100000 100001 | ADD R0, R1 |
|A001|              |RET|
|A002| 1011 000000 0000000 1010 0000 0000 0000| CALL 0xA000


## Hora de pensar

Supongamos que tenemos la siguiente rutina ensamblada a partir de la celda `3344`:

```
miRutina: SUB R6, 0xAAAA
          RET
```

> ¿Cómo es el código máquina de la instrucción `CALL miRutina`?
