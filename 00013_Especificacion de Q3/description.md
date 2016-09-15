# Formatos de Instruccion

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-7geq{background-color:#ffffc7;text-align:center;vertical-align:top}
.tg .tg-quxf{background-color:#ffffff;text-align:center;vertical-align:top}
</style>

## Instrucciones de 2 operandos

<table class="tg">
  <tr>
    <th class="tg-7geq">codop</th>
    <th class="tg-7geq">modo Destino<br></th>
    <th class="tg-7geq">modo Origen<br></th>
    <th class="tg-7geq">operando Destino<br></th>
    <th class="tg-7geq">operando Origen<br></th>
  </tr>
  <tr>
    <td class="tg-quxf">4 bits<br></td>
    <td class="tg-quxf">6 bits<br></td>
    <td class="tg-quxf">6 bits<br></td>
    <td class="tg-quxf">16 bits<br></td>
    <td class="tg-quxf">16 bits</td>
  </tr>
</table>

## Instrucciones de 1 Operando Origen

<table class="tg">
  <tr>
    <th class="tg-7geq">codop</th>
    <th class="tg-7geq">Relleno<br></th>
    <th class="tg-7geq">modo Origen<br></th>
    <th class="tg-7geq">operando Origen<br></th>
  </tr>
  <tr>
    <td class="tg-quxf">4 bits<br></td>
    <td class="tg-quxf">000000<br></td>
    <td class="tg-quxf">6 bits<br></td>
    <td class="tg-quxf">16 bits</td>
  </tr>
</table>

## Instrucciones sin operandos


# Tablas de Codigos de Operación

<table class="tg">
  <tr>
    <th class="tg-7geq">Instrucción</th>
    <th class="tg-7geq">Tipo</th>
    <th class="tg-7geq">Codop<br></th>
    <th class="tg-7geq">Efecto<br></th>
  </tr>
  <tr>
    <td class="tg-quxf">MUL</td>
    <td class="tg-quxf">2 operandos<br></td>
    <td class="tg-quxf">0000 </td>
    <td class="tg-quxf">Dest=Dest*Origen </td>
  </tr>
  <tr>
    <td class="tg-baqh">MOV</td>
    <td class="tg-baqh">2 operandos<br></td>
    <td class="tg-baqh">0001</td>
    <td class="tg-baqh">Dest=Origen </td>
  </tr>
  <tr>
    <td class="tg-sh4c">ADD</td>
    <td class="tg-sh4c">2 operandos<br></td>
    <td class="tg-sh4c">0010</td>
    <td class="tg-sh4c">Dest=Dest+Origen </td>
  </tr>
  <tr>
    <td class="tg-baqh">SUB</td>
    <td class="tg-baqh">2 operandos<br></td>
    <td class="tg-baqh">0011</td>
    <td class="tg-baqh">Dest=Dest-Origen</td>
  </tr>
  <tr>
    <td class="tg-sh4c">DIV</td>
    <td class="tg-sh4c">2 operandos<br></td>
    <td class="tg-sh4c">0111</td>
    <td class="tg-sh4c">Dest=Dest%Origen</td>
  </tr>
  <tr>
    <td class="tg-baqh">CALL</td>
    <td class="tg-baqh">1 op. destino<br></td>
    <td class="tg-baqh">1011</td>
    <td class="tg-baqh">[SP]=PC; SP=SP-1; PC=Origen</td>
  </tr>
  <tr>
    <td class="tg-sh4c">RET</td>
    <td class="tg-sh4c">sin operandos<br></td>
    <td class="tg-sh4c">1100</td>
    <td class="tg-sh4c">SP=SP+1; PC=[SP]</td>
  </tr>


# Modos de direccionamiento