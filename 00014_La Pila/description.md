### Idea

En la ejecución de un programa las instrucciones se toman en el orden que tienen físicamente en la Memoria Principal. Para esto la UC tiene en cuenta el valor del **registro PC**. Supongamos el siguiente caso:

![PC inicial](https://raw.githubusercontent.com/Orga-UNQ/mumuki-guia-q3-rutinas/master/images/motivacionPC.png "PC inicial")


¿Cómo supone hace el sistema para realizar el “desvío” en el call rutinaA? ¿Como supone hace el sistema para que el RET en rutinaA permita ejecutar el segundo CALL? (siguiente instrucción del último llamado)

**Durante** la ejecución de la instrucción ```CALL```, el PC debe ser alterado para que **la siguiente instrucción sea** la de la etiqueta rutinaA. Pero ojo! El PC debe ser guardado antes de que ocurra lo anterior, para que el RET funcione adecuadamente.

Ahora aparece la siguiente pregunta: **¿Donde se “salva” el PC para hacer el RET?**

Una posible solución es tener otro registro de uso específico (por ejemplo PC2) para usar en el RET. Es decir:
1. cuando hay un call:

```
PC2 <- PC
PC <- dirección de la etiqueta rutinaA
```
2. Cuando se alcanza el ret:

```
PC<-PC2
```

¿Cuando no es suficiente esta solución?

Veamos este caso: Si se salva el PC cuando se ejecuta el call rutinaA, entonces en el call rutinaB se pierde el valor guardado. Entonces hacemos otra propuesta: Agregar otro registro para salvar el segundo valor de PC. Cómo sería el protocolo entonces?
1. Cuando hay un call:

```
PC3<-PC2; 
PC2 <- PC
PC <- dirección de la etiqueta
```
2.cuando se alcanza el ret:
```
PC<-PC2; 
PC2<-PC3
```
¿Cuál es el problema de esto? La cantidad de CALLs que pueden “encadenarse” o “anidarse” está limitada al conjunto de registros PCx (es una estructura estática)

### Les presento… una pila

Para solucionar este problema utilizaremos una *estructura de datos* (o una forma de organizar/estructurar un conjunto de datos) que se denomina **PILA**. Esta estructura puede pensarse como una pila de platos, es decir que los datos se manejan siempre desde el tope de la pila, dando lugar a las siguientes operaciones sobre la pila:

1. Poner un plato en la pila, denominado **APILAR** (push), es decir agregar un elemento sobre el último elemento agregado.
2. Retirar un plato de la pila, denominado **DESAPILAR** (pop) es decir  se le  saca del "tope" o primer plato de la pila.

Esta forma de operar determina qu no se pueda sacar datos que no estén en el tope ni pueden agregarse datos por el medio de la pila.


#### La pila en la memoria

Imaginemos que esta nueva estructura de datos la guardamos en una zona especial de memoria que va a ser **accedida solamente apilando y desapilando**.
(Ver en el siguiente gráfico que el tope de pila está resaltado en **negrita**)

|    | ...  |
|--- |---|
|FFE9|????|
|FFEA|????|
|FFEB|????|
|FFEC|????|
|FFED|????|
|FFEE|????|
|**FFEF**|????|
|    |  ... |



Asumimos que la pila comienza en la dirección **FFEF** de memoria. Pensemos que pasa al apilar el dato BBBB en dicha pila: Luego de esto el tope de pila es **FFFE**, para que el tope de pila represente en todo momento, **el primer lugar disponible sobre los valores ya apilados**.Gráficamente:


|    | ...  |
|--- |---|
|FFE9|????|
|FFEA|????|
|FFEB|????|
|FFEC|????|
|FFED|????|
|**FFEE**|????|
|FFEF|BBBB|
|    |  ... |

Eso implica que con cada push se debe **decrementar** la dirección que indica el tope de pila (Ver donde está el tope en el gráfico anterior).

Ahora agregamos el elemento 1002 ¿donde queda el tope de pila? Graficamente:


|    | ...  |
|--- |---|
|FFE9|????|
|FFEA|????|
|FFEB|????|
|FFEC|????|
|**FFED**|????|
|FFEE|1002|
|FFEF|BBBB|
|    |  ... |

Supongamos que ahora se quiere **desapilar** (hacer un pop). El tope de pila debe ajustarse y luego debe copiarse el dato, porque el **invariante** es que el tope de pila representa el primer lugar disponible sobre los valores ya apilados.

¿De que manera? ahora el tope de pila debe **incrementarse**, como se grafica:


|    | ...  |
|--- |---|
|FFE9|????|
|FFEA|????|
|FFEB|????|
|FFEC|????|
|**FFED**|????|
|FFEE|1002|
|FFEF|BBBB|
|    |  ... |


#### ¿Y dónde está el tope de pila?

Como vemos, en todo momento necesitamos saber dónde se encuentra el tope de pila, entonces para su seguimiento usaremos un registro especial llamado **SP** (*Stack Pointer*). Este registro contiene la dirección de la primer celda de memoria disponible de la pila (cumple con el invariante mencionado).
Entonces las operaciones de la pila son:

* **Push**: Es una escritura en memoria.
  1. Escribe el dato que en la dirección que está en SP 
  2. y se decrementa SP, para dejar todo listo al nuevo tope de pila.
* **Pop**: Es una lectura de memoria
  1. Se incrementa SP (para que haga referencia a un dato dentro de la pila)
  2. Se hace una lectura de la dirección que está en SP


### Atención

Algunos detalles a tener en cuenta:

1. El tamaño y la ubicación de la pila está definido por la arquitectura. En nuestro caso en Q3 comienza en FFFE, pero no en todas las arquitecturas eso es necesariamente asi.
2. El pop no *blanquea* (elimina el contenido de) el tope de la pila sino que, por definición de cómo funcionan push y pop, ese dato ya no se puede acceder.


## ¿ Cómo relacionamos esto con  CALL y RET?

Recordemos que:

* Instrucción CALL: Desvía el flujo del programa a la instrucción que define la etiqueta.
* Instrucción RET: Permite restituir el flujo del programa a la instrucción siguiente del último llamado.

Para que esto sea posible se utiliza un pila, donde la instrucción que produce un push es ```CALL```, y la que produce un pop es ```RET```. Detallemos un poco:

* La instrucción```CALL``` apila la dirección de la siguiente instrucción. Durante la etapa de *ejecución de instrucción*  (ver [ciclo revisado](http://orga-unq.mumuki.io/exercises/2920-ejecucion-de-programas-memoria-buses-y-q2-paso-a-paso)) dicha dirección está en el registro PC 
* La instrucción ```RET``` desapila para actualizar **PC**

### Seguimiento de la ejecución

Para hacer el seguimiento de la ejecución, confeccionaremos una tabla que nos permitirá mostrar como varían los registros PC y SP durante la ejecución de un programa:

```
rutina1: MOV R1, R0
         RET

programa: CALL rutina1
          CALL rutina1
```

Para este ejemplo necesitamos saber:

* rutina1 está ensamblada a partir de la celda 0x00E0
* programa está ensamblado a partir de la celda 0x1000
* PC inicialmente vale 1000
* La pila está vacía (es decir, SP=FFEF


<table class="table"><thead>
<tr>
<th>Instruccion</th>
<th>Busqueda de Instrucción</th>
<th  colspan="3">Ejecución de Instrucción</th>
</tr>
<tr>
<th></th>
<th>PC sig. inst.</th>
<th>Tope</th>
<th>SP</th>
<th>PC</th>
</tr>
</thead><tbody>
<tr>
<td><code>CALL rutina1</code></td>
<td>1002</td>
<td>00E0</td>
<td>FFEE</td>
<td>1002</td>
</tr>
<tr>
<td><code>MOV R1, R0</code></td>
<td>00E1</td>
<td>00E1</td>
<td>FFEE</td>
<td>1002</td>
</tr>
<tr>
<td><code>RET</code></td>
<td>00E2</td>
<td>1002</td>
<td>FFEF</td>
<td>-</td>
</tr>
<tr>
<td><code>CALL rutina1</code></td>
<td>1004</td>
<td>00E0</td>
<td>FFEE</td>
<td>1004</td>
</tr>
<tr>
<td><code>MOV R1, R0</code></td>
<td>00E1</td>
<td>00E1</td>
<td>FFEE</td>
<td>1004</td>
</tr>
<tr>
<td><code>RET</code></td>
<td>00E2</td>
<td>1004</td>
<td>FFEF</td>
<td>-</td>
</tr>
</tbody>
</table>

