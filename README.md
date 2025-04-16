# Premiação do Oscar
Dentro do arquivo "Oscar2025.json", contém os dados dos indicados ao OSCAR do ano de 1928 a 2025, colocados dentro do banco de dados "MongoDB".

A seguir, há um questionários para trabalhar e treinar os comandos CRUD.

--- 

* Atualize os registros da tabela com os dados do Oscar 2025
  
  R: Registros Atualizados!

---

* Qual o **total** de registros na tabela indicados?

   R: 11009 Registros.

---

* Qual o número de indicações por categoria agrupadas por categoria?
 R: 20 Indicações por categoria agrupadas

Code:
```js
db.indicados_ao_oscar.aggregate([
  {
    $group: {
      _id: "$categoria",  
      total_indicacoes: { $sum: 1 }  
    }
  },
  {
    $sort: { total_indicacoes: -1 } 
  }
]);
```

---

* Quantas vezes Natalie Portman foi indicada ao Oscar?
  R: 3

Code:
```js
db.oscar.countDocuments({"nome_do_indicado": "Natalie Portman"})
````
---

* Quantos Oscars Natalie Portman ganhou?
  R: 1

Code:
```js
db.oscar.countDocuments({
nome_do_indicado: "Natalie Portman",
vencedor: "true"
})
```

---

* Quantas vezes Viola Davis foi indicada ao Oscar?
  R: 4

Code:
```js
db.oscar.countDocuments({"nome_do_indicado": "Viola Davis"})
```
---

* Quantos Oscars Viola Davis ganhou?
  R: 1

Code:
```js
db.oscar.countDocuments({
nome_do_indicado: "Viola Davis",
vencedor: "true"
})
```
---

* Amy Adams já ganhou algum Oscar?
  R: Não

Code: 
```js
db.oscar.countDocuments({
nome_do_indicado: "Amy Adams",
vencedor: "true"
})
```

---

* Quais os atores/atrizes que foram indicados mais de uma vez?
  R: 1446

Code:
```js
 db.oscar.aggregate([
  { $group: { _id: "$nome_do_indicado", total_indicacoes: { $sum: 1 } } },
  { $match: { total_indicacoes: { $gt: 1 } } },
  { $count: "quantidade_atores_mais_uma_indicacao" }
])
```

---

* A série de filmes Toy Story ganhou Oscars em quais anos?
  R: 2 vezes em 2011 e 1 em 2020

Code:
```js
 db.registros.find({
nome_do_filme: /Toy Story/,
vencedor: "true"
})
```

---

* A partir de que ano que a categoria "Actress" deixa de existir?
  R: Apartir do ano de 1928

Code:
```js
 db.registros.find({
categoria: "ACTRESS" ,
vencedor: "true"
}).sort({
ano_cerimonia: 1
}).limit(1)
```

---

* Quem ganhou o primeiro Oscar para Melhor Atriz? Em que ano?

---

* Na campo "Vencedor", altere todos os valores com "true" para 1 e todos os valores "false" para 0.

---

* Em qual edição do Oscar "Crash" concorreu ao Oscar?

---

* O filme Central do Brasil aparece no Oscar?

---

* Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser. 

---

* Denzel Washington já ganhou algum Oscar?

---

* Quais os filmes que ganharam o Oscar de Melhor Filme?

---

* Sidney Poitier foi o primeiro ator negro a ser indicado ao Oscar. Em que ano ele foi indicado? Por qual filme?

---

* Quais os filmes que ganharam o Oscar de Melhor Filme e Melhor Diretor na mesma cerimonia?

---

* Denzel Washington e Jamie Foxx já concorreram ao Oscar no mesmo ano?
