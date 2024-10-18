<h1>Atividade Oscar</h1>	




1- Quantas vezes Natalie Portman foi indicada ao Oscar?

R: Natalie foi indicada 3 vezes ao oscar
```
Q: db["registro"].countDocuments({nome_do_indicado: "Natalie Portman"})
```

2- Quantos Oscars Natalie Portman ganhou?

R: A Natalie levou para casa 1 Oscar
```
Q: db["registro"].countDocuments({nome_do_indicado: "Natalie Portman", vencedor: "true" })
```

3- Amy Adams já ganhou algum Oscar?

R: Não, Amy Adams nunca ganhou um Oscar.
```
Q: db["registro"].countDocuments({nome_do_indicado: "Amy Adams", vencedor: "true" })
```

4- A série de filmes Toy Story ganhou um Oscar em quais anos?

R: A franquia de filmes Toy Story levou Oscar nos anos de 2011 e 2020
```
Q: db.registro.find({nome_do_filme: /Toy Story/, vencedor: "true"})
```

5-

R: deixa de existir em 1976
```
db.Oscar.find({categoria: 'ACTRESS'}, {ano_cerimonia: 1, categoria: 1, _id: 0}).sort({
ano_cerimonia: -1
}).limit(1)
```

6- O  primeiro Oscar para melhor Atriz foi para quem? Em que ano?

R: foi em 1928
```
Q: db.Oscar.find({categoria: "ACTRESS", vencedor: 'true'}, {ano_cerimonia: 1, categoria: 1, nome_do_indicado: 1}).limit(1)
```

7-  Na campo "Vencedor", altere todos os valores com "Sim" para 1 e todos os valores "Não" para 0.

R: ok
```
Q: db.registros.updateMany({vencedor: "false"}, {$set: {vencedor: 0}});
db.registros.updateMany({vencedor: "true"}, {$set: {vencedor: 1}});
```

8- Em qual edição do Oscar "Crash" concorreu ao Oscar?

R: na edição de numero 78
```
Q: db.registros.distinct('cerimonia', {nome_do_filme: 'Crash'})
```

9- Bom... dê um Oscar para um filme que merece muito, mas não ganhou.

R:darei o oscar paa o filme Cidade de Deus...
```
Q: db.Oscar.updateOne({vencedor: 1, ano_cerimonia: 2004}, {$set: {vencedor: 0}})
db.Oscar.updateOne({nome_do_filme: "City of God", ano_cerimonia: 2004}, {$set: {vencedor: 1}})
```

10- O filme Central do Brasil aparece no Oscar?

R: sim, aparece em duas categorias, melhor atriz e melhor filme internacional
```
Q:O filme Central do Brasil aparece no Oscar?
```

11- inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas merecem ser.

R: adicionei Carandiru, Estomago e Que horas ela volta
```
db.Oscar.insertMany([{
ano_filmagem: 2003,
ano_cerimonia: 2004,
cerimonia: 76,
categoria: "Best Picture",
nome_do_indicado: "Fernando Meirelles",
nome_do_filme: "Carandiru",
vencedor: 0
},
{
ano_filmagem: 2007,
ano_cerimonia: 2008,
cerimonia: 80,
categoria: "Best Picture",
nome_do_indicado: "Marcos Jorge",
nome_do_filme: Estômago, a Gastronomic Story",
vencedor: 0
},
{
ano_filmagem: 2015,
ano_cerimonia: 2016,
cerimonia: 88,
categoria: "Best Picture",
nome_do_indicado: "Anna Muylaert",
nome_do_filme: "The Second Mother",
vencedor: 0
}])
```

12 - Pensando no ano em que você nasceu: Qual foi o Oscar de melhor filme, Melhor Atriz e Melhor Diretor?

R:o melhor filme foi Menina de Ouro, a Melhor Atriz foi a Hillary Swank pelo filme Menina de Ouro e o Melhor Diretor o Clint Eastwood
```
Q:db.Oscar.find({ano_cerimonia: 2005, vencedor: 1, categoria: { "$in": ["ACTRESS IN A LEADING ROLE", "BEST PICTURE", "DIRECTING"]}}, {categoria: 1, nome_do_indicado: 1, _id: 0})
```
