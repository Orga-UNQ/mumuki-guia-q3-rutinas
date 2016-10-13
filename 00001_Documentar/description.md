### Comunicarse entre programadores

Es importante que veas la necesidad de acompañar tu programa con el correspondiente texto que describa **Que hace** y **Que necesita**. ¿Cual es el problema de no acompañar el código con esa documentación?

* Para entender la intención o el objetivo de la rutina es necesario leer el código, y muchas veces no está disponible
* Es difícil saber cómo usar la rutina
* Es difícil modificar el código para nuevos requerimientos y asegurar que no aporta errores secundarios. Pensemos que nosotros modificamos registros que son globales a todos los programas.

#### Formato de la documentación
Un posible método/protocolo de documentación es como sigue:


<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;border-color:#aaa;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:#aaa;color:#333;background-color:#fff;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:#aaa;color:#fff;background-color:#f38630;}
.tg .tg-j2zy{background-color:#FCFBE3;vertical-align:top}
.tg .tg-rmb8{background-color:#C2FFD6;vertical-align:top}
.tg .tg-yw4l{vertical-align:top}
</style>

<table class="tg">
  <tr>
    <th class="tg-yw4l">Requiere<br></th>
    <td class="tg-yw4l"> Describe qué necesita la rutina (parámetros y precondiciones) ¿Donde están los parámetros?¿Que características deben tener?</th>
  </tr>
  <tr>
    <th class="tg-yw4l">Modifica</td>
    <td class="tg-yw4l">Describe qué variables (registros, memoria) auxiliares se utilizan ¿Cambia alguna variable que no es el resultado? ¿Cambian las variables con los parámetros de entrada?</td>
  </tr>
  <tr>
    <th class="tg-yw4l">Retorna</td>
    <td class="tg-yw4l">Describe en qué variable (registro o memoria) se retorna el resultado. ¿Que caracteristicas es importante marcar del resultado?</td>
  </tr>
</table>

Veamos un ejemplo. Considerá la siguiente rutina:


```
prom: MOV R0, R4
      ADD R0, R5
      DIV R0, 0x0002
      MOV R6, R0
```

La documentación podría ser:


```
Requiere:  en R4 y R5 los dos valores a promediar
Modifica: el registro R0
Retorna: en el registro R6 el promedio de ambos valores
```


#### A poner en práctica

Documentá la siguiente rutina. 

```
promedio: ADD R5, R6
      DIV R5, 0x0002
      MOV R1, R5
```

Completando el siguiente texto:


```
Requiere:  
Modifica:
Retorna: 
```
