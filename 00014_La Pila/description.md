### Idea

En la ejecución de un programa las instrucciones se toman en el orden que tienen físicamente en la Memoria Principal. Para esto la UC tiene en cuenta el valor del **registro PC**. Supongamos el siguiente caso:

![PC inicial](https://raw.githubusercontent.com/Orga-UNQ/mumuki-guia-q3-rutinas/master/images/motivacionPC.png "PC inicial")


¿Cómo supone hace el sistema para realizar el “desvío” en el call rutinaA? ¿Como supone hace el sistema para que el RET en rutinaA permita ejecutar el segundo CALL? (siguiente instrucción del último llamado)

**Durante** la ejecución de la instrucción ```CALL```, el PC debe ser alterado para que **la siguiente instrucción sea** la de la etiqueta rutinaA. Pero ojo! El PC debe ser guardado antes de que ocurra lo anterior, para que el RET funcione adecuadamente.


### Estructura de datos: La pila
