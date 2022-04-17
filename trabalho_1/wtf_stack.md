# Processador de Pilhas, Oque comem, Ondem vivem, Oque fazem?

Processadores são sistemas que recebem uma sequencia de intruções e as realizam.
Estão inclusos operações operações aritimetica e desvio de fluxo.

Diferente dos processadores mais usuais que tem varios registradores,
o registrados de pilha tem apenas dois e realiza todas as operações em
cima de uma pilha. Podendo acrescentar valores na pilha e operar em cima deles.

Por exemplo o seguinte programa:
```
1 IM 0x27
2 IM 0x1A
3 ADD
5 NOT
```

O `IM` carrega um valor imediato (um valor q vc já sabe, q tá na instrução)
para a pilha.

Executando `IM 0x27` (Linha 0) temos a pilha:

|      |
|------|
| 0x27 |

OBS: Estou abstraindo algumas coisas aqui então não leve em consideração o tamanho das coisas ainda)

Depois com `IM 0x1A` (Linha 1):

|      |
|------|
| 0x1A |
| 0x27 |

Então temos a instrução `ADD` (Linhas 2) que é uma soma, como a soma é um operador binario
(soma dois numeros) ele vai pegar os dois valores do topo da pilha (0x1A + 0x27)
e retornar com o resultado (0x41):

|      |
|------|
| 0x41 |

E então uma instrução unaria `NOT` (Linha 4) q pega um unico parametro:

|      |
|------|
| 0xBE |
