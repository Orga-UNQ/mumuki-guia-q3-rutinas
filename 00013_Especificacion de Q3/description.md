# Formatos de Instruccion

## Instrucciones de 2 operandos

## Instrucciones de 1 Operando Origen

|[codop]|[relleno]|[Modo Origen]|[Operando Origen]|
|:-------:|---------|-------------|----------------|
| 4b    | 000000  |   6b        | 16 b           |

## Instrucciones sin operandos


# Tablas de Codigos de Operación


| Instrucción | codop | Efecto    | Tipo |
|:-----------:|:-----:|:---------:|:----:|
| MUL         | 0000  | `Dest<-Dest*Origen`| inst de dos operandos|
| MOV         | 0001  | `Dest<-Origen`| inst de dos operandos|
| ADD         | 0010  | `Dest<-Dest+Origen`| inst de dos operandos|
| SUB         | 0000  | `Dest<-Dest-Origen`| inst de dos operandos|
| DIV         | 0111  | `Dest<-Dest/Origen`| inst de dos operandos|
| CALL        | 1011  | `[SP]<-PC; SP<-SP-1; PC<--Origen` | inst. de un operando origen |
| RET         | 1100  | `SP<-SP+1; PC<--[SP]` | inst. de un operando origen |



# Modos de direccionamiento