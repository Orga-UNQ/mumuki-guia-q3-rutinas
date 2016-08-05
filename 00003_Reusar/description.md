# La vida es repetir... y reusar

Supongamos que se necesita construir un programa que calcule n⁵ para los números almacenados en las celdas A001, A002 y A003 y lo guarde en las mismas celdas. Por ejemplo,

El primer paso para resolverlo es modularizar y plantear 3 rutinas:


```
pot5A1: MOV R1, [0xA001]
        MUL R1, [0xA001]
        MUL R1, [0xA001]
        MUL R1, [0xA001]
        MUL R1, [0xA001]
        MOV [0xA001], R1
        RET
pot5A2: MOV R1, [0xA002]
        MUL R1, [0xA002]
        MUL R1, [0xA002]
        MUL R1, [0xA002]
        MUL R1, [0xA002]
        MOV [0xA002], R1
        RET
pot5A3: MOV R1, [0xA003]
        MUL R1, [0xA003]
        MUL R1, [0xA003]
        MUL R1, [0xA003]
        MUL R1, [0xA003]
        MOV [0xA003], R1
        RET
```




Entonces es posible **rescatar un patrón**:

1.Copiar el contenido de [x] a un registro,
2.multiplicarlo 4 veces por sí mismo y 
3.guardar el resultado en [x]


(Antes)[2534-ejecucion-de-programas-q3-rutinas-dividir-en-subrutinas] dijimos que una rutina es un programa que resuelve un problema acotado, pero ahora podemos agregar que son muy útiles para resolver problemas **recurrentes**

Entonces, algunas rutinas son pensadas para poder ser usadas en múltiples ocasiones. 

Trabajemos sobre el ejemplo: el código de la rutina puede ser como sigue:

```
pot5: MOV R1, [0xA001]
      MUL R1, [0xA001]
      MUL R1, [0xA001]
      MUL R1, [0xA001]
      MUL R1, [0xA001]
      MOV [0xA001], R1
```

configurando un pasaje de parámetros
¿Cómo se integran las partes o rutinas? Se necesita hacer dos cosas:
Encapsular las rutinas: delimitar comienzo y fin. Para esto se utiliza una etiqueta y una instrucciòn especial RET
comienzo: etiqueta que la identifique unívocamente
fin: instrucción RET


escribir un programa...