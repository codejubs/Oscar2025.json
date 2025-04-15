# Premiação do Oscar
Dentro do arquivo "Oscar2025.json", contém os dados dos indicados ao OSCAR do ano de 1928 a 2025, colocados dentro do banco de dados "MongoDB".

A seguir, há um questionários para trabalhar e treinar os comandos CRUD.


* Atualize os registros da tabela com os dados do Oscar 2025
  - Registros Atualizados!
--------------------------------------------------------
 * Qual o total de registros na tabela indicados?
  - 11009 Registros.
--------------------------------------------------------
 * Qual o número de indicações por categoria agrupadas por categoria?
  - 20 Indicações por categoria agrupadas

*code:    
db.registros.aggregate([
  { $group: { _id: "$categoria", totalIndicacoes: { $sum: 1 } } },
  { $sort: { totalIndicacoes: -1 } }
]);
--------------------------------------------------------

