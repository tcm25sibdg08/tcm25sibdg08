# SQL

## DDL

DROP VIEW IF EXISTS v_OcupacaoSessao; 

DROP TABLE IF EXISTS Bilhete; 

DROP TABLE IF EXISTS Sessao; 

DROP TABLE IF EXISTS Cliente; 

DROP TABLE IF EXISTS Sala; 

DROP TABLE IF EXISTS Filme;



### CREATE TABLE Filme ( 
    id_filme INT AUTO_INCREMENT PRIMARY KEY, 

    titulo VARCHAR(255) NOT NULL, 

    duracao INT NOT NULL, 

    genero ENUM('Ação', 'Comédia', 'Drama', 'Terror', 'Sci-Fi', 'Animação') NOT NULL 
);

### CREATE TABLE Sala ( 
    id_sala INT AUTO_INCREMENT PRIMARY KEY, 

    nome VARCHAR(100) NOT NULL, 

    capacidade INT NOT NULL 
);

### CREATE TABLE Cliente ( 
    id_cliente INT AUTO_INCREMENT PRIMARY KEY, 

    nome VARCHAR(255) NOT NULL, 

    email VARCHAR(255) UNIQUE NOT NULL 
);

### CREATE TABLE Sessao ( 
    id_sessao INT AUTO_INCREMENT PRIMARY KEY, 

    horario DATETIME NOT NULL, 

    id_filme INT NOT NULL, 

    id_sala INT NOT NULL, 

    FOREIGN KEY (id_filme) REFERENCES Filme(id_filme), 

    FOREIGN KEY (id_sala) REFERENCES Sala(id_sala), 

    UNIQUE KEY uq_sala_horario (id_sala, horario) 
);

### CREATE TABLE Bilhete ( 
    id_bilhete INT AUTO_INCREMENT PRIMARY KEY, 

    quantidade INT NOT NULL CHECK (quantidade > 0), 

    id_cliente INT NOT NULL, 

    id_sessao INT NOT NULL, 

    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente), 

    FOREIGN KEY (id_sessao) REFERENCES Sessao(id_sessao) 
);

### CREATE VIEW v_OcupacaoSessao AS 
SELECT 

    s.id_sessao, 

    f.titulo AS filme, 

    sl.nome AS sala, 

    sl.capacidade AS lotacao_total, 

    IFNULL(SUM(b.quantidade), 0) AS bilhetes_vendidos, 

    (sl.capacidade - IFNULL(SUM(b.quantidade), 0)) AS lugares_disponiveis 

FROM Sessao s 

JOIN Filme f ON s.id_filme = f.id_filme 

JOIN Sala sl ON s.id_sala = sl.id_sala 

LEFT JOIN Bilhete b ON s.id_sessao = b.id_sessao 

GROUP BY s.id_sessao;


## DML (Data Manipulation Language)

Nesta secção, são apresentados exemplos de consultas SQL que respondem aos requisitos funcionais do sistema, permitindo a gestão e consulta de dados tanto por parte do Administrador como do Cliente.

### 1. Consulta de Filmes em Exibição (Catálogo)

Descrição do Requisito: O cliente necessita de consultar os filmes disponíveis, os seus géneros e os horários das sessões.

Query:
SELECT f.titulo, f.genero, s.horario, sl.nome AS sala

FROM Filme f

JOIN Sessao s ON f.id_filme = s.id_filme

JOIN Sala sl ON s.id_sala = sl.id_sala

ORDER BY s.horario ASC;

Resultado Expectável: Uma lista de filmes com o respetivo género (validado pelo tipo ENUM), horário e nome da sala onde será exibido.

--------------------------------------------------------------------------------
### 2. Verificação de Lugares Disponíveis (Regra de Negócio)

Descrição do Requisito: Antes de realizar uma compra, o sistema deve verificar se a sessão ainda tem lugares livres, recorrendo à vista de ocupação.

Query:
SELECT filme, sala, lugares_disponiveis 

FROM v_OcupacaoSessao 

WHERE id_sessao = 5; -- Exemplo para a sessão com ID 5

Resultado Expectável: Uma linha que indica o nome do filme, a sala e o cálculo exato de lugares_disponiveis (Capacidade - Bilhetes Vendidos) para a sessão selecionada.

--------------------------------------------------------------------------------
### 3. Histórico de Compras de um Cliente

Descrição do Requisito: Permite consultar todos os bilhetes e quantidades adquiridas por um cliente específico através do seu email único.

Query:
SELECT c.nome, f.titulo, s.horario, b.quantidade

FROM Cliente c

JOIN Bilhete b ON c.id_cliente = b.id_cliente

JOIN Sessao s ON b.id_sessao = s.id_sessao

JOIN Filme f ON s.id_filme = f.id_filme

WHERE c.email = 'utilizador@email.com';

Resultado Expectável: Uma listagem detalhada com o nome do utilizador, os filmes comprados e a quantidade de ingressos em cada compra.

--------------------------------------------------------------------------------
### 4. Relatório de Faturação por Filme (Administração)

Descrição do Requisito: O administrador pretende saber o total de bilhetes vendidos para cada filme no catálogo.

Query:
SELECT f.titulo, SUM(b.quantidade) AS total_vendido

FROM Filme f

LEFT JOIN Sessao s ON f.id_filme = s.id_filme

LEFT JOIN Bilhete b ON s.id_sessao = b.id_sessao

GROUP BY f.id_filme, f.titulo;

Resultado Expectável: Uma tabela com todos os filmes e o somatório total de bilhetes vendidos para cada um, independentemente da sala ou horário.

--------------------------------------------------------------------------------
### 5. Verificação de Conflitos de Sala

Descrição do Requisito: Validar se a regra de integridade que impede duas sessões na mesma sala à mesma hora está a ser cumprida.

Query:
SELECT id_sala, horario, COUNT(*) 

FROM Sessao 

GROUP BY id_sala, horario 

HAVING COUNT(*) > 1;

Resultado Expectável: Como existe uma restrição UNIQUE KEY uq_sala_horario no esquema, esta consulta deverá retornar sempre 0 resultados, confirmando que não há sobreposição de sessões.

---
[< Previous](rebd03.md) | [^ Main](/../../) | Next >
:--- | :---: | ---: 