Atividade Prática – MongoDB: Antes e Depois
Objetivo
Praticar os principais comandos do MongoDB analisando o estado da coleção antes e produzindo o estado depois por meio de operações no banco de dados.

Cenário
Você foi contratado para administrar o banco de dados de uma loja online.

Crie um banco chamado store e uma coleção chamada customers.
use store
db.createCollection("customers")

Insira os seguintes documentos:

db.customers.insertMany (
[
  {
    "name": "Ana",
    "age": 25,
    "city": "Salvador",
    "active": true,
    "points": 120
  },
  {
    "name": "Bruno",
    "age": 32,
    "city": "Feira de Santana",
    "active": true,
    "points": 300
  },
  {
    "name": "Carlos",
    "age": 28,
    "city": "Salvador",
    "active": false,
    "points": 80
  },
  {
    "name": "Daniela",
    "age": 40,
    "city": "São Paulo",
    "active": true,
    "points": 500
  },
  {
    "name": "Eduarda",
    "age": 22,
    "city": "Rio de Janeiro",
    "active": false,
    "points": 50
  }
])
 
Exercício 1 – Consulta
Antes
Todos os documentos acima.

Depois
Resultado esperado:

[
  {
    "name": "Ana",
    "city": "Salvador"
  },
  {
    "name": "Carlos",
    "city": "Salvador"
  }
]
Sua tarefa

Escreva o comando MongoDB que produz esse resultado.
db.customers.find({"city": "Salvador"})


Exercício 2 – Atualização
Antes
{
  "name": "Carlos",
  "active": false
}
Depois
{
  "name": "Carlos",
  "active": true
}
Sua tarefa

Escreva o comando necessário.
db.customers.updateOne({"name": "Carlos" }, { $set: { "active": true }})

Exercício 3 – Atualizar vários documentos
Antes
{
  "city": "Salvador"
}
Depois
Todos os clientes de Salvador passam a possuir:

"state": "BA"
Sua tarefa

Escreva o comando.
db.customers.updateMany({"city":"Salvador"}, {$set: {"state": "BA"}})

Exercício 4 – Incremento
Antes
{
  "name": "Ana",
  "points": 120
}
Depois
{
  "name": "Ana",
  "points": 170
}
Sua tarefa

Escreva o comando utilizando o operador mais adequado.
db.customers.updateOne({"name": "Ana"}, {$inc: { "points": 50}})

Exercício 5 – Inserção
Antes
A coleção possui cinco documentos.

Depois
A coleção passa a possuir mais um documento:

{
  "name": "Fernando",
  "age": 29,
  "city": "Recife",
  "active": true,
  "points": 90
}
Sua tarefa

Escreva o comando.

db.customers.insertOne ({
  "name": "Fernando",
  "age": 29,
  "city": "Recife",
  "active": true,
  "points": 90
})


Exercício 6 – Remoção
Antes
Existe o cliente:

{
  "name": "Eduarda"
}
Depois
O documento não existe mais.

Sua tarefa

Escreva o comando.
db.customers.deleteOne({"name": "Eduarda"})


Exercício 7 – Criar um novo campo
Antes
{
  "name": "Daniela"
}
Depois
{
  "name": "Daniela",
  "vip": true
}
Sua tarefa

Escreva o comando.
db.customers.updateOne({"name": "Daniela"}, {$set: {"vip":"true"}})


Exercício 8 – Remover um campo
Antes
{
  "name": "Bruno",
  "points": 300
}
Depois
{
  "name": "Bruno"
}
O campo points não deve mais existir.

Sua tarefa

Escreva o comando.
db.customers.updateOne({"name": "Bruno"}, {$unset: {"points": ""}})


Exercício 9 – Ordenação
Antes
Todos os documentos.

Depois
Os clientes aparecem ordenados por idade em ordem decrescente.

Sua tarefa

Escreva o comando.
db.customers.find().sort({"age": -1})

Exercício 10 – Filtro com múltiplas condições
Antes
Todos os documentos.

Depois
Resultado esperado:

[
  {
    "name": "Bruno"
  },
  {
    "name": "Daniela"
  }
]
Somente clientes ativos com mais de 30 anos.

Sua tarefa

Escreva o comando.
db.costumers.find({$and:[{"age": {$gt: 30}},{"active": true}]})

Desafio
Sem alterar os documentos existentes, escreva comandos para obter os seguintes resultados:

1. Mostrar apenas os nomes dos clientes
db.customers.find(
  {},
  { "_id": 0, "name": 1 }
)

2. Contar quantos clientes existem
db.customers.countDocuments()

3. Contar apenas os clientes ativos
db.customers.countDocuments({
  "active": true
})

4. Mostrar o cliente com maior pontuação
db.customers.find().sort({
  "points": -1
}).limit(1)

5. Mostrar o cliente com menor idade
db.customers.find().sort({
  "age": 1
}).limit(1)

6. Mostrar apenas clientes com pontuação entre 100 e 400
db.customers.find({
  "points": {
    $gte: 100,
    $lte: 400
  }
})

7. Mostrar apenas clientes das cidades de Salvador ou São Paulo
db.customers.find({
  "city": {
    $in: ["Salvador", "São Paulo"]
  }
})

8. Mostrar todos os clientes ordenados por nome
db.customers.find().sort({
  "name": 1
})

9. Mostrar apenas os três primeiros clientes
db.customers.find().limit(3)

10. Mostrar apenas os clientes inativos
db.customers.find({
  "active": false
})