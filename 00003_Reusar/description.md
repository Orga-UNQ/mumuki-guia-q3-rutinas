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


¿Cómo es el programa *cliente* de esas rutinas?

```
CALL potA001
CALL potA002
CALL potA003
```

En particular en este ejercicio, sospechamos que es posible ahorrar trabajo, pues vemos que hay mucho en común entre las tres rutinas. 

Entonces es posible **rescatar un patrón**:

1. Copiar el valor a procesar a un registro,
2. multiplicarlo 4 veces por sí mismo y 
3. guardar el resultado en la celda que corresponda


(Antes)[2534-ejecucion-de-programas-q3-rutinas-dividir-en-subrutinas] dijimos que una rutina es un programa que resuelve un problema acotado, pero ahora podemos agregar que son muy útiles para resolver problemas **recurrentes**

Entonces, algunas rutinas son pensadas para poder ser usadas en múltiples ocasiones. 

¿Cómo sería esa rutina? 

```
pot5: MOV R1, ?
      MUL R1, ?
      MUL R1, ?
      MUL R1, ?
      MUL R1, ?
      MOV ?, R1
```

Bueno, pero este código no es correcto en Q3. 

# Configurando parámetros

Aquello que varía en el ejemplo anterior (`?`) se denomina **parámetro**, y es una variable cuyo valor se debe configurar previamente a la llamada de la rutina. 

Para que sea parametrizable, una posibilidad es que la rutina anterior tome como parámetro el valor en el registro R0 y se reescribe:

```
pot5: MOV R1, R0
      MUL R1, R0
      MUL R1, R0
      MUL R1, R0
      MUL R1, R0
      MOV R0, R1
```

Entonces ¿Cómo se invoca esta subrutina?

# Pasando parámetros

Sabiendo que `pot5` espera en R0 el valor a *elevar a la quinta*, su invocación es como sigue:

```
MOV R0, [0xA001]
CALL pot5
```
# Recuperando resultados

Usando la rutina de la manera que se indica, el resultado queda en R0 y no en la celda A001, como se necesitaba. Por lo tanto, luego de terminada la ejecución de la rutina, se debe guardar el resultado adecuadamente:

```
MOV R0, [0xA001]
CALL pot5
MOV  [0xA001], R0
```

# Pasando en limpio


```
pot5: MOV R1, R0
      MUL R1, R0
      MUL R1, R0
      MUL R1, R0
      MUL R1, R0
      MOV R0, R1
```

Programa principal:
```
MOV R0, [0xA001]
CALL pot5
MOV  [0xA001], R0
MOV R0, [0xA002]
CALL pot5
MOV  [0xA002], R0
MOV R0, [0xA002]
CALL pot5
MOV  [0xA002], R0
```


# A trabajar