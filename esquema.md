# C3 : Esquema conceptual

## Modelo E/A

## Entidades-tipo:

Filme (id_filme, duracao, genero, titulo)

Sessão (id_sessao, horario)

Sala (id_sala, capacidade, nome)

Cliente (id_cliente, nome, email)

Bilhete (id_bilhete, quantidade)


## Associações:

éExibidoEm (FILME, SESSAO)       1:N        total/parcial

ocorreEm (SESSAO, SALA)          N:1        total/parcial

compra (CLIENTE, BILHETE)        1:N        total/parcial

correspondeA (BILHETE, SESSAO)   N:1        total/parcial


![An alternative description](diagrama.PNG)   

Esta imagem é o Diagrama do modelo Entidade-Associação.

## Explicação rápida (Associações):

éExibidoEm (FILME, SESSAO)
Um filme pode ter várias sessões

ocorreEm (SESSAO, SALA)
Cada sessão acontece numa sala

compra (CLIENTE, BILHETE)
Um cliente pode comprar vários bilhetes

correspondeA (BILHETE, SESSAO)
Cada bilhete pertence a uma sessão

---
[< Previous](requisitos.md) | [^ Main](/../../) | Next >
:--- | :---: | ---: 