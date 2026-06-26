# Normalização

# Do Modelo EA a Relação

## Modelo Relacional

Filme (id_filme, titulo, duracao, genero),

Sala (id_sala, nome, capacidade),

Sessao (id_sessao, horario, id_filme, id_sala),

(Nota: id_filme e id_sala são chaves estrangeiras que ligam a sessão ao respetivo filme e sala.)

Cliente (id_cliente, nome, email),

Bilhete (id_bilhete, quantidade, id_cliente, id_sessao),

(Nota: id_cliente e id_sessao são chaves estrangeiras que registam quem comprou e para que sessão.)

[< Previous](rebd01.md) | [^ Main](/../../) | [Next >](rebd03.md)
:--- | :---: | ---: 