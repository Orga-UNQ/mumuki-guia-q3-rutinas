# La vida es repetir... y reusar

Supongamos que se necesita construir un programa que calcule n⁵ para los números almacenados en las celdas A001, A002 y A003 y lo guarde en las mismas celdas. Por ejemplo,



```
MOV R1, [0xA001]
MUL R1, [0xA001]
MUL R1, [0xA001]
MUL R1, [0xA001]
MUL R1, [0xA001]
MOV [0xA001], R1
MOV R1, [0xA002]
MUL R1, [0xA002]
MUL R1, [0xA002]
MUL R1, [0xA002]
MUL R1, [0xA002]
MOV [0xA002], R1
MOV R1, [0xA003]
MUL R1, [0xA003]
MUL R1, [0xA003]
MUL R1, [0xA003]
MUL R1, [0xA003]
MOV [0xA003], R1
```

Entonces es posible rescatar un patrón


Copiar el contenido de [x] a un registro,
multiplicarlo 4 veces por sí mismo y 
guardar el resultado en [x]




partir el problema 

y/o **recurrente**. Entonces, es pensada para poder ser usada en múltiples ocasiones. De esta manera, permite reusar la idea de la solución y además permite partir el problema. También la llamaremos subrutina, pues en general se la utiliza como parte (subparte) de un programa más grande y específico.
Modularizar: Dividir el problema grande en problemas más chicos. Conectarlo con el primer ejercicio: En ese caso las rutinas son dos distintas, pero que permiten acotar el análisis y el pensamiento de la solución para abordarlo mejor.
Reusar: Pensar la solución para que se adapte a distintas situaciones. Conectarlo con el segundo ejercicio: En ese caso la rutina es una sola, y se aplica a distintas celdas, configurando un pasaje de parámetros
¿Cómo se integran las partes o rutinas? Se necesita hacer dos cosas:
Encapsular las rutinas: delimitar comienzo y fin. Para esto se utiliza una etiqueta y una instrucciòn especial RET
comienzo: etiqueta que la identifique unívocamente
fin: instrucción RET


escribir un programa...