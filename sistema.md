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


<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <title>Sistema de Gestão de Cinema - Pesquisa</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        input { width: 100%; padding: 12px; margin-bottom: 20px; border: 1px solid #ddd; }
        table { width: 100%; border-collapse: collapse; }
        th, td { padding: 12px; border: 1px solid #ddd; text-align: left; }
        tr:nth-child(even) { background-color: #f9f9f9; }
        .header { background-color: #007bff; color: white; }
    </style>
</head>
<body>

    <h2>Consulta de Sessões e Ocupação</h2>
    
    <!-- Caixa de Pesquisa que filtra por qualquer coluna -->
    <input type="text" id="inputPesquisa" onkeyup="pesquisarTabela()" placeholder="Pesquise por filme, sala, género ou data...">

    <table id="tabelaCinema">
        <tr class="header">
            <th>Filme</th>
            <th>Género</th>
            <th>Sala</th>
            <th>Data/Horário</th>
            <th>Ocupação (Vendidos/Total)</th>
            <th>Lugares Disponíveis</th>
        </tr>
        <!-- Dados baseados nos requisitos de centralização e controlo [1-3] -->
        <tr>
            <td>Inception</td>
            <td>Sci-Fi</td>
            <td>Sala IMAX</td>
            <td>2024-06-20 18:30</td>
            <td>45 / 150</td>
            <td>105</td>
        </tr>
        <tr>
            <td>Toy Story</td>
            <td>Animação</td>
            <td>Sala 3</td>
            <td>2024-06-20 15:00</td>
            <td>10 / 100</td>
            <td>90</td>
        </tr>
        <tr>
            <td>Dune: Part Two</td>
            <td>Sci-Fi</td>
            <td>Sala IMAX</td>
            <td>2024-06-20 21:00</td>
            <td>5 / 150</td>
            <td>145</td>
        </tr>
        <tr>
            <td>The Conjuring</td>
            <td>Terror</td>
            <td>Sala VIP</td>
            <td>2024-06-21 22:00</td>
            <td>0 / 40</td>
            <td>40</td>
        </tr>
    </table>

    <script>
    function pesquisarTabela() {
        var input = document.getElementById("inputPesquisa").value.toUpperCase();
        var table = document.getElementById("tabelaCinema");
        var tr = table.getElementsByTagName("tr");

        // Começa em 1 para saltar o cabeçalho
        for (var i = 1; i < tr.length; i++) {
            var mostrar = false;
            var td = tr[i].getElementsByTagName("td");
            
            // Percorre todas as colunas da linha para ver se há correspondência
            for (var j = 0; j < td.length; j++) {
                if (td[j]) {
                    var texto = td[j].textContent || td[j].innerText;
                    if (texto.toUpperCase().indexOf(input) > -1) {
                        mostrar = true;
                        break; // Para se encontrar correspondência em qualquer coluna
                    }
                }
            }
            tr[i].style.display = mostrar ? "" : "none";
        }
    }
    </script>
</body>
</html>