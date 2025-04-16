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
 db.oscar.find({
nome_do_filme: /Toy Story/,
vencedor: "true"
})
```

---

* A partir de que ano que a categoria "Actress" deixa de existir?
  
  R: Apartir do ano de 1928

Code:
```js
 db.oscar.find({
categoria: "ACTRESS" ,
vencedor: "true"
}).sort({
ano_cerimonia: 1
}).limit(1)
```

---

* Quem ganhou o primeiro Oscar para Melhor Atriz? Em que ano?
  R: Janet Gaynor no ano de 1928!

Code:
```js
db.oscar.find({
categoria: "ACTRESS" ,
vencedor: "true"
}).sort({
ano_cerimonia: 1
})
```

---

* Na campo "Vencedor", altere todos os valores com "true" para 1 e todos os valores "false" para 0.
  R: Alteração realizada!

Code:
```js
db.oscar.updateMany({
   vencedor: "false"
}, {
    $set: {
       vencedor: "0"
    }
});

db.oscar.updateMany({
   vencedor: "true"
}, {
    $set: {
       vencedor: "1"
    }
});
```

---

* Em qual edição do Oscar "Crash" concorreu ao Oscar?
  R: Edição: 78

Code:
```js
db.oscar.find({
nome_do_filme: "Crash"
})
```
  

---

* O filme Central do Brasil aparece no Oscar?
  R: Não

Code: 
```js
db.oscar.find({
nome_do_filme: "Central do Brasil"
})
```
  

---

* Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser. 

---

* Denzel Washington já ganhou algum Oscar?
  R: Sim, 2 Oscars

Code:
```js
db.oscar.countDocuments({
nome_do_indicado: "Denzel Washington",
vencedor: "1"
})
```

---

* Quais os filmes que ganharam o Oscar de Melhor Filme?
  R: Going My Way, The Lost Weekend, The Best Years of Our Lives, Gentleman's Agreement, Hamlet, All the King's Men, All about Eve, An American in Paris, The Greatest Show on Earth, From Here to Eternity, On the Waterfront, Marty, Around the World in 80 Days, The Bridge on the River Kwai, Gigi, Ben-Hur, The Apartment, West Side Story.

Code:
```js
db.oscar.find({
categoria: "BEST MOTION PICTURE",
vencedor: "1"
})
```


---

* Sidney Poitier foi o primeiro ator negro a ser indicado ao Oscar. Em que ano ele foi indicado? Por qual filme?
  R: 1959 com o filme "The Defiant Ones" e 1964 com o filme "Lilies Of The Field"

Code:
```js
db.oscar.find({
nome_do_indicado: "Sidney Poitier"
})
```
  

---

* Quais os filmes que ganharam o Oscar de Melhor Filme e Melhor Diretor na mesma cerimonia?

---

* Denzel Washington e Jamie Foxx já concorreram ao Oscar no mesmo ano?
