-- 1. Inserir Filmes (Catálogo)
INSERT INTO Filme (titulo, duracao, genero) VALUES 
('Inception', 148, 'Sci-Fi'),
('O Padrinho', 175, 'Drama'),
('Toy Story', 81, 'Animação'),
('The Conjuring', 112, 'Terror'),
('Dune: Part Two', 166, 'Sci-Fi');

-- 2. Inserir Salas de Cinema
-- Note que definimos a capacidade para controlar a ocupação [4]
INSERT INTO Sala (nome, capacidade) VALUES 
('Sala IMAX', 150),
('Sala VIP', 40),
('Sala 3', 100);

-- 3. Inserir Clientes
INSERT INTO Cliente (nome, email) VALUES 
('João Silva', 'joao.silva@email.com'),
('Maria Santos', 'maria.santos@email.com'),
('Pedro Oliveira', 'pedro.oliveira@email.com');

-- 4. Inserir Sessões
-- Cada sessão corresponde a um filme e uma sala específica [4]
-- Respeitando a regra de não haver conflitos de horário na mesma sala [3]
INSERT INTO Sessao (horario, id_filme, id_sala) VALUES 
('2024-06-20 15:00:00', 3, 3), -- Toy Story na Sala 3
('2024-06-20 18:30:00', 1, 1), -- Inception na Sala IMAX
('2024-06-20 21:00:00', 5, 1), -- Dune na Sala IMAX
('2024-06-21 22:00:00', 4, 2); -- The Conjuring na Sala VIP

-- 5. Inserir Vendas de Bilhetes
-- O sistema foca na quantidade adquirida por cliente [2]
INSERT INTO Bilhete (quantidade, id_cliente, id_sessao) VALUES 
(3, 1, 1), -- João comprou 3 bilhetes para Toy Story
(2, 2, 2), -- Maria comprou 2 bilhetes para Inception
(1, 3, 2), -- Pedro comprou 1 bilhete para Inception
(5, 1, 3); -- João comprou 5 bilhetes para Dune