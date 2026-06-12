# Esquema Relacional


Nesta secção, apresenta-se a definição física da base de dados, detalhando cada tabela, as suas colunas e as restrições de integridade que garantem a consistência do sistema de cinema.

### Relações

- Filme

- Sala

- Sessao

- Cliente

- Bilhete

- Vistas

--------------------------------------------------------------------------------
## Filme

### DESCRIÇÃO 

Armazena os dados dos filmes em exibição, incluindo a restrição de domínio para o género.

| Nome | Descrição | Domínio | por Omissão | Automático | Nulo |
| :--- | :--- | :--- | :--- | :--- | :--- |
| id_filme | Identificador do filme | INT | - | Sim | Não |
| titulo | Título da obra | VARCHAR(255) | - | Não | Não |
| duracao | Duração em minutos | INT | - | Não | Não |
| genero | Género cinematográfico | ENUM* | - | Não | Não |

RESTRIÇÕES DE INTEGRIDADE

Chave Primária: id_filme

--------------------------------------------------------------------------------
## Sala

### DESCRIÇÃO 

Regista as salas de cinema e a sua lotação máxima.

| Nome | Descrição | Domínio | por Omissão | Automático | Nulo |
| :--- | :--- | :--- | :--- | :--- | :--- |
| id_sala | Identificador da sala | INT | - | Sim | Não |
| nome | Nome ou número da sala | VARCHAR(100) | - | Não | Não |
| capacidade | Total de lugares | INT | - | Não | Não |

RESTRIÇÕES DE INTEGRIDADE

Chave Primária: id_sala

--------------------------------------------------------------------------------
## Sessao

### DESCRIÇÃO 

Define o horário em que um filme é exibido numa determinada sala.

| Nome | Descrição | Domínio | por Omissão | Automático | Nulo |
| :--- | :--- | :--- | :--- | :--- | :--- |
| id_sessao | Identificador da sessão | INT | - | Sim | Não |
| horario | Data e hora da sessão | DATETIME | - | Não | Não |
| id_filme | Referência ao filme | INT | - | Não | Não |
| id_sala | Referência à sala | INT | - | Não | Não |

RESTRIÇÕES DE INTEGRIDADE

Chave Primária: id_sessao

Referencial (Chaves Estrangeiras):
fk_sessao_filme: id_filme -> Tabela Filme (id_filme)
fk_sessao_sala: id_sala -> Tabela Sala (id_sala)

--------------------------------------------------------------------------------
## Cliente

### DESCRIÇÃO 

Contém os dados dos utilizadores que utilizam o sistema para comprar bilhetes.

| Nome | Descrição | Domínio | por Omissão | Automático | Nulo |
| :--- | :--- | :--- | :--- | :--- | :--- |
| id_cliente | Identificador do cliente | INT | - | Sim | Não |
| nome | Nome completo | VARCHAR(255) | - | Não | Não |
| email | E-mail do utilizador | VARCHAR(255) | - | Não | Não |

RESTRIÇÕES DE INTEGRIDADE

Chave Primária: id_cliente

Unicidade:
email_unique: email (Indexar: Sim)

--------------------------------------------------------------------------------
## Bilhete

### DESCRIÇÃO 

Regista a compra autónoma efetuada pelo cliente para uma sessão específica.

| Nome | Descrição | Domínio | por Omissão | Automático | Nulo |
| :--- | :--- | :--- | :--- | :--- | :--- |
| id_bilhete | Identificador do bilhete | INT | - | Sim | Não |
| quantidade | Número de ingressos | INT | - | Não | Não |
| id_cliente | Referência ao cliente | INT | - | Não | Não |
| id_sessao | Referência à sessão | INT | - | Não | Não |
RESTRIÇÕES DE INTEGRIDADE

Chave Primária: id_bilhete

Referencial (Chaves Estrangeiras):
fk_bilhete_cliente: id_cliente -> Tabela Cliente (id_cliente)
fk_bilhete_sessao: id_sessao -> Tabela Sessao (id_sessao)

--------------------------------------------------------------------------------
## Vistas

v_OcupacaoSessao

### DESCRIÇÃO 

Vista obrigatória que calcula o nível de ocupação da sala, cruzando a capacidade da sala com a soma de bilhetes vendidos por sessão.

| Coluna | Descrição | Origem |
| :--- | :--- | :--- |
| id_sessao | ID da sessão | Sessao.id_sessao |
| filme | Nome do filme | Filme.titulo |
| sala | Nome da sala | Sala.nome |
| total_lugares | Capacidade da sala | Sala.capacidade |
| ocupados | Lugares vendidos | SUM(Bilhete.quantidade) |
| disponiveis | Lugares livres | (Capacidade - Ocupados) |

< [Previous](rebd02.md) | [^ Main](/../../) | [Next >](rebd04.md)
:--- | :---: | ---: 