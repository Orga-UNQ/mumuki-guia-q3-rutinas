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


escribir un programa...