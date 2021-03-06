# Explicando os valores parciais

## Simbolos
| Simbolo | Nome              | Exemplo                   |
|---------|-------------------|---------------------------|
| <<      | left shift        | "0001" << 2 = "0100"      |
| \|      | or logico         | "0110" \| "1100" = "0100" |
| &       | concatenação      | "10" & "01" = "1001"      |
| signExt | extensor de sinal | signExt("10", 4) = "1110" |

## not(ir[4])&ir[3:0]«2
Inverte o primeiro bit e concatena com os 4 bits menos significativos shiftados pra esquerda

Como ele vai pra ula de 32 bits vc pode considerar q o shift não zera a saida (é melhor implementar como concat),
lembrando que vai ter que dar um resize para ficar do mesmo tamanho da ula.

Em vhdl: `(not ir(4)) & ir(3 downto 0) & "00"`

## memA_rdd«7 | IR[6:0]
Aqui estamos deslocando a a memoria 7 bits pro lado, e dps fazemos um OR nesses 7 bits
(que vão ser zero, então só vai ser 1 onde vir 1 do IR).

Ex:
```
memA_rdd = 0000 0001 1011 0011
ir       =           1010 1010

memA_rdd << 7 = 1101 1001 1000 0000
ir[6:0]       =            010 1010
|             = 1101 1001 1010 1010
```

Observe que podemos obter o mesmo resultado concatenando e truncando o resultado


Em vhdl: `(memA_rdd sll 7) or ir(6 downto 0)` ou `memA_rdd(24 downto 0) & ir(6 downto 0)`

## signExt(ir[6:0])
Quando estamos extendendo um numero para "caber" em uma bit_vector
maior precisamos levar em conta o sinal,
quando extendemos um numero positivo basta adicionar zero a esquerda,
entretando quando extendemos um numero negativo precisamos adicionar 1 a esquerda (para manter o sinal e o valor em complemento de 2).

Ex:
```vhdl
signExt("1100", 8) = "11111100" -- -4 em complemento de 2
signExt("0010", 8) = "00000010" -- 2
```

Dica: Você pode criar um componente ou usar a função resize com signed

## Observação

Lembre q no seu dataflow esses tamanhos são genericos, então muito dos valores
aqui devem ser parametrizados. Você tamém pode usar a função resize da numeric_bit.
