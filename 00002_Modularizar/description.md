# Divide y triunfarás

Supongamos que debemos escribir un programa que calcule lo siguiente

`R6=(95+R1)*18 + R1/(R2+256)`

Una forma de abordarlo es tomarlo como dos problemas de menor complejidad:

Término A | Término B
--- | --- 
`(95+R1)*18` | `R1/(R2+256)`

```
MOV R2, 0x005F
ADD R2, R1
MUL R2, 0x0012
```
Una rutina es un programa que resuelve un problema acotado y recurrente. Entonces, es pensada para poder ser usada en múltiples ocasiones. De esta manera, permite reusar la idea de la solución y además permite partir el problema. También la llamaremos subrutina, pues en general se la utiliza como parte (subparte) de un programa más grande y específico.
Modularizar: Dividir el problema grande en problemas más chicos. Conectarlo con el primer ejercicio: En ese caso las rutinas son dos distintas, pero que permiten acotar el análisis y el pensamiento de la solución para abordarlo mejor.
Reusar: Pensar la solución para que se adapte a distintas situaciones. Conectarlo con el segundo ejercicio: En ese caso la rutina es una sola, y se aplica a distintas celdas, configurando un pasaje de parámetros
¿Cómo se integran las partes o rutinas? Se necesita hacer dos cosas:
Encapsular las rutinas: delimitar comienzo y fin. Para esto se utiliza una etiqueta y una instrucciòn especial RET
comienzo: etiqueta que la identifique unívocamente
fin: instrucción RET

Escribir un programa 