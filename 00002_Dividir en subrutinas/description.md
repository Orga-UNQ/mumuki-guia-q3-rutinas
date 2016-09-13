
# Divide y triunfarás

Supongamos que debemos escribir un programa que calcule lo siguiente

`R6=(95+R1)*18 + R4/(R2+256)`

Una forma de abordarlo es tomarlo como dos problemas de menor complejidad:

Término A | Término B
--- | --- 
`(95+R1)*18` | `1/(R2+256)`

Entonces, el código que resuelve el termino A podría ser:

```
MOV R3, 0x005F 
ADD R3, R1
MUL R3, 0x0012 
```

Y el correspondiente al término B:

```
ADD R2, 0x0100 
MOV R4, 0x0001
DIV R4, R2
```

Una rutina es un programa que resuelve un problema **acotado**, y el diseño de programas usando rutinas (también llamadas subrutinas) permite simplificar las soluciones. Es decir que deben identificar las partes para luego resolver cada una independientemente y luego **componerlas**.


# Diseño por partes

¿Cómo se diseña el programa usando rutinas? Se necesita hacer dos cosas: *encapsular* las rutinas y luego *invocar*

## Encapsular las rutinas

El encapsulamiento no es ni mas ni menos que la tarea de delimitar comienzo y fin de la rutina. Para esto se utiliza una etiqueta y una instrucciòn especial RET

* Al comienzo: La etiqueta es un texto (seguido por ":") que identifique la rutina unívocamente, y que se coloca junto a la primer instrucción.
* Al final: instrucción RET. Este instrucción provoca que el flujo de programa vuelva a **la instrucción siguiente al último CALL**


Por ejemplo, siguiendo el ejemplo de arriba las rutinas se encapsulan como sigue:

```
rutA: MOV R3, 0x005F 
      ADD R3, R1
      MUL R3, 0x0012 
      RET
```
```
rutB: ADD R2, 0x0100 
      MOV R4, 0x0001
      DIV R4, R2
      RET
```

## Invocar las rutinas

El lenguaje Q3 provee una instrucción CALL que desvía el flujo del programa hacia la instrucción marcada con la etiqueta
Recuperando el ejemplo, las rutinas se invocan de la siguiente manera:

```
CALL rutA
CALL rutB
```

# A trabajar

Se tiene la siguiente rutina:

```
rutInicializadora: MOV R4,0x0010
                   RET
```
> Escribir un programa que llame a la rutina anterior