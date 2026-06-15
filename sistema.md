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


<!-- Caixa de Pesquisa -->
<input type="text" id="inputPesquisa" onkeyup="pesquisarFilme()" placeholder="Pesquisar por título ou género...">

<table id="tabelaFilmes">
  <tr class="header">
    <th>Filme</th>
    <th>Género</th>
    <th>Sala</th>
  </tr>
  <!-- Os dados aqui viriam da sua tabela 'Filme' e 'Sessao' -->
  <tr>
    <td>Inception</td>
    <td>Sci-Fi</td>
    <td>Sala IMAX</td>
  </tr>
  <tr>
    <td>Toy Story</td>
    <td>Animação</td>
    <td>Sala 3</td>
  </tr>
</table>

<script>
function pesquisarFilme() {
  var input = document.getElementById("inputPesquisa").value.toUpperCase();
  var table = document.getElementById("tabelaFilmes");
  var tr = table.getElementsByTagName("tr");

  for (var i = 1; i < tr.length; i++) {
    var td = tr[i].getElementsByTagName("td"); // Coluna do Título
    if (td) {
      var texto = td.textContent || td.innerText;
      tr[i].style.display = texto.toUpperCase().indexOf(input) > -1 ? "" : "none";
    }
  }
}
</script>