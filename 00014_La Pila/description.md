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

