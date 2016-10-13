Recordemos una vez mas que la instrucción ```RET``` permite restituir el flujo del programa a la instrucción siguiente del último llamado. Esto se consigue mediante el efecto:

```
SP = SP + 1
PC = [SP]
```

Esto implica que el **operando destino**, así como el **operando origen** estén implícitos, y esto la convierte en una instrucción sin operandos, con el siguiente formato:



<table class="tg">
  <tr>
    <th class="tg-7geq">codop</th>
    <th class="tg-7geq">Relleno<br></th>
  </tr>
  <tr>
    <td class="tg-quxf">4 bits<br></td>
    <td class="tg-quxf">000000000000<br></td>
  </tr>
</table>


# A pensar

¿Cuantas celdas ocupa una instrucción ```RET```?