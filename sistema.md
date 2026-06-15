# Sistema de Gestão de Cinema - Base de Dados

## 1. Catálogo de Filmes
| Título | Duração (min) | Género |
| :--- | :---: | :--- |
| Inception | 148 | Sci-Fi |
| O Padrinho | 175 | Drama |
| Toy Story | 81 | Animação |
| The Conjuring | 112 | Terror |
| Dune: Part Two | 166 | Sci-Fi |

## 2. Salas e Capacidade
*Controlo de lotação conforme os requisitos do sistema [1].*
| Nome da Sala | Capacidade |
| :--- | :---: |
| Sala IMAX | 150 |
| Sala VIP | 40 |
| Sala 3 | 100 |

## 3. Horários das Sessões
*Garantia de que não existem conflitos de horários na mesma sala [3].*
| Horário | Filme | Sala |
| :--- | :--- | :--- |
| 2024-06-20 15:00 | Toy Story | Sala 3 |
| 2024-06-20 18:30 | Inception | Sala IMAX |
| 2024-06-20 21:00 | Dune: Part Two | Sala IMAX |
| 2024-06-21 22:00 | The Conjuring | Sala VIP |

## 4. Histórico de Bilhetes Vendidos
*Venda baseada na quantidade, sem atribuição de lugar específico [1, 3].*
| Cliente | Filme | Quantidade |
| :--- | :--- | :---: |
| João Silva | Toy Story | 3 |
| Maria Santos | Inception | 2 |
| Pedro Oliveira | Inception | 1 |
| João Silva | Dune: Part Two | 5 |


