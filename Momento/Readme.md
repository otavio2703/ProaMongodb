# Atividade Momento

#### 1. Quantos funcionarios da empresa Momento trabalham no departamento de vendas?</br>
<strong>Resposta:</strong> tem ao todo no setor de vendas 10 funcionarios.


```javascript
db.funcionarios.countDocuments({ "cargo": /vendas/i })
```
<hr>

#### 2. Inclua suas próprias informações no departamento de Tecnologia da empresa.</br>
<strong>Resposta:</strong> feito 👍

```js
db.funcionarios.insertMany([
    {
        "nome": "Otavio Gonçalves",
        "telefone": "(11) 99159-1658",
        "email": "otaviocgoncalve@gmail.com",
        "dataAdmissao": "2005-03-27",
        "cargo": "Analista de dados",
        "salario": 2700000,
        "departamento": ObjectId("85992103f9b3e0b3b3c1fe74"),
    }
]);

```
<hr>

#### 3. Agora diga, quantos funcionários temos ao total na empresa?</br>
<strong>Resposta:</strong> ao todo na empresa tem 24 funcionários, contando comigo.

```js
db.funcionarios.countDocuments()
```
<hr>

#### 4. E quanto ao Departamento de Tecnologia?</br>
<strong>Resposta:</strong> tem 6 funcionários no departamento de tecnologia.

```js
db.funcionarios.countDocuments({"departamento": ObjectId("85992103f9b3e0b3b3c1fe74")})
```
<hr>

#### 5. Qual a média salarial do departamento de tecnologia?</br>
<strong>Resposta:</strong> a média ficou em R$453.800.

```js
db.funcionarios.aggregate([
    {
        $match: {"departamento": ObjectId("85992103f9b3e0b3b3c1fe74")}
    },
    {
        $group: {
            _id: null,
            media_de_salario: { $avg: "$salario" }
        }
    }
])
```
<hr>

#### 6. Quanto o departamento de Vendas gasta em salários?</br>
<strong>Resposta:</strong>  Ao todo a empresa gasta em salário no setor de vendas R$95.100.

```js
db.funcionarios.aggregate([
    {
        $match: { "cargo": /vendas/i }
    },
    {
        $group: {
            _id: null,
            gasto_em_salario: { $sum: "$salario" }
        }
    }
])
```
<hr>

#### 7. Um novo departamento foi criado. O departamento de Inovações. Ele será locado no Brasil. Por favor, adicione-o no banco de dados da empresa colocando quaisquer informações que você achar relevantes.</br>
<strong>Resposta:</strong> O departamento foi adicionado.

```js
db.departamentos.insertOne({
    "_id": ObjectId("85992103f9b3e0b3b3c1fe74"),
    "nome": "Inovações",
    "escritorio": ObjectId("5f8b3f3f9b3e0b3b3c1e3e3e")
});
```
<hr>

#### 8. O departamento de Inovações está sem funcionários. Inclua alguns colegas de turma nesse departamento.</br>
<strong>Resposta:</strong> Adicionei os membros do meu grupo de demo-day.👍

```js
db.funcionarios.insertMany([
    {
        "nome": "Malcoln Lucas",
        "telefone": "(11) 98759-5071",
        "email": "Malcolnhatsunemiku@gmail.com",
        "dataAdmissao": "2003-06-27",
        "cargo": "Programação 2",
        "salario": 11133,
        "departamento": ObjectId('66f1c0efd15d5494e3f31947'),
    },
    {
        "nome": "Glenda Alves",
        "telefone": "(11) 94080-2315",
        "email": "glendinhaalvessccp@gmail.com",
        "dataAdmissao": "2015-03-04",
        "cargo": "café com leite",
        "salario": 13111,
        "departamento": ObjectId('66f1c0efd15d5494e3f31947')
    },
    {
        "nome": "Francielly Menezes",
        "telefone": "(11) 99653-0342",
        "email": "franmenguista@gmail.com",
        "dataAdmissao": "2017-02-30",
        "cargo": "samengo",
        "salario": 12113,
        "departamento": ObjectId('66f1c0efd15d5494e3f31947'),
    },
    {
        "nome": "Guilherme Francisco",
        "telefone": "(11) 93085-2172",
        "email": "guilhermereidelas@gmail.com",
        "dataAdmissao": "2022-08-16",
        "cargo": "reidelas",
        "salario": 1500,
        "departamento": ObjectId('66f1c0efd15d5494e3f31947'),
    },
    {
        "nome": "Jonathan dos Anjos",
        "telefone":  "(11) 98705-7200",
        "email": "jhowjhowdelas@gmail.com",
        "dataAdmissao": "2019-05-08",
        "cargo": "comunicador",
        "salario": 13000,
        "departamento": ObjectId('66f1c0efd15d5494e3f31947'),
    },
    {
        "nome": "Miriã Moreno",
        "telefone": "(11) 91116-1868",
        "email": "miriapickmegirl@gmail.com",
        "dataAdmissao": "2016-04-20",
        "cargo": "pick me girl",
        "salario": 13111,
        "departamento": ObjectId('66f1c0efd15d5494e3f31947')
    }
]);

```
<hr>

#### 9. Quantos funcionarios a empresa Momento tem agora?</br>
<strong>Resposta:</strong> Até o momento a empresa tem 30 funcionários.

```js
db.funcionarios.countDocuments()
```
<hr>

#### 10. Quantos funcionários da empresa Momento possuem conjuges?</br>
<strong>Resposta:</strong> Ao que tudo indica a consulta me retornou 7 pessoas com cônjuges.

```js
db.funcionarios.aggregate([
    { $match: { "dependentes.conjuge": { $exists: true } } },
    { $count: "totalFuncionariosComConjuge" }
])
```
<hr>

#### 11. Qual a média salarial dos funcionários da empresa Momento, excluindo-se o CEO?</br>
<strong>Resposta:</strong> A média salarial de todos os funcionários é R$102.712

```js
db.funcionarios.aggregate([
    {
        $match: {
            cargo: { $ne: "CEO" }
        }
    },
    {
        $group:{
            _id: null,
            mediaSalarial: { $avg: "$salario" }
        }
    } 
])
```
<hr>

#### 12. Qual a média salarial do departamento de tecnologia?</br>
<strong>Resposta:</strong> A média salarial do departamento de tecnologia é R$453.800

```js
db.funcionarios.aggregate([
    {
        $match: { "departamento": ObjectId("85992103f9b3e0b3b3c1fe74") }
    },
    {
        $group: {
            _id: null,
            a_media_salarial: { $avg: "$salario" }
        }
    }
])

```
<hr>

#### 13. Qual o departamento com a maior média salarial?</br>
<strong>Resposta:</strong> É o departamento de Tecnologias.

```js
db.funcionarios.aggregate([
    {
        $group: {
            _id: "$departamento",
            mediaSalarial: { $avg: "$salario" }
        }
    },
    {
        $lookup: {
            from: "departamentos",
            localField: "_id",            
            foreignField: "_id",
            as: "informacoesDepartamento"
        }
    },
    {
        $sort: { mediaSalarial: -1 }
    },
    {
        $limit: 1
    },
    {
        $project: {
            _id: 0,
            mediaSalarial: 1,
            "informacoesDepartamento.nome": 1
        }
    }
])

```
<hr>

#### 14. Qual o departamento com o menor número de funcionários?</br>
<strong>Resposta:</strong> É o executivo.

```js
db.funcionarios.aggregate([
    {
        $group: {
            _id: "$departamento",
            totalFuncionarios: { $sum: 1 }
        }
    },
    {
        $lookup: {
            from: "departamentos",
            localField: "_id",
            foreignField: "_id",
            as: "infoDepartamento"
        }
    },
    {
        $sort: { totalFuncionarios: 1 }
    },
    {
        $limit: 1
    },
    {
        $project: {
            _id: 0,
            totalFuncionarios: 1,
            nomeDepartamento: { $arrayElemAt: ["$infoDepartamento.nome", 0] }
        }
    }
])
```
<hr>

#### 15. Pensando na relação quantidade e valor unitario, qual o produto mais valioso da empresa?</br>
<strong>Resposta:</strong> R$ 95.000, o produto mais valioso na empresa são os computadores do departamento de marketing.

```js
db.escritorios.aggregate([
    {
        "$unwind": "$suprimentos"
    },
    {
        "$lookup": {
            "from": "departamentos",
            "localField": "departamento",
            "foreignField": "_id",
            "as": "infoDepartamento"
        }
    },
    {
        "$group": {
            "_id": "$suprimentos",
            "quantidade": { "$sum": 1 },
            "valorUnitario": { "$avg": "$infoDepartamento.preco" }
        }
    },
    {
        "$sort": {
                "quantidade": -1,
                "valorUnitario": -1
            }
    }
])

```
<hr>

#### 16. Qual o produto mais vendido da empresa?</br>
<strong>Resposta:</strong> É o laço da verdade, vendeu 12 unidades

```js
> db.vendas.aggregate([
    {
        "$group": {
            "_id": "$produto",
            "count": { $sum: "$quantidade" }
        }
    },
    {
        "$sort": { "count": -1 }
    },
    {
        "$limit": 1
    }
])

< {
  _id: 'Laço da Verdade',
  count: 12
  }
```
<hr>

#### 17. Qual o produto menos vendido da empresa?</br>
<strong>Resposta:</strong> Com apenas duas vendas é o 'Fake Batarang'

```js
db.vendas.aggregate([
    {
        "$group": {
            "_id": "$produto",
            "totalQuantidade": { "$sum": "$quantidade" },
            "totalVendas": { "$sum": { "$multiply": ["$quantidade", "$precoUnitario"] } }
        }
    },
    {
        "$sort": { "totalQuantidade": 1 }
    },
    {
        "$limit": 1
    },
    {
        "$project": {
            "_id": 0,
            "produto": "$_id",
            "totalQuantidade": 1,
            "totalVendas": 1
        }
    }
]);


```
<hr>
