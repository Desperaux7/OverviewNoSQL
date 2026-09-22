# Guia de Fundamentos: NoSQL e MongoDB

## 1. Conceitos Básicos de Banco de Dados Orientado a Documentos

A estrutura de organização dos dados segue uma hierarquia definida:

* **Database:** O banco de dados em si, que pode hospedar múltiplas coleções.
* **Collection (Coleção):** Agrupamento de documentos.
* **Document (Documento):** Onde os dados são efetivamente armazenados.

## 2. Estrutura de Dados: JSON e BSON

Os documentos são manipulados e armazenados utilizando formatos baseados em chave-valor.

* **JSON:** Delimitado por chaves `{}`.
* **Campos (Fields):** Consistem em uma chave (ou nome) e um valor, separados por dois-pontos `:`. Múltiplos campos são separados por vírgulas.
* **Tipos de Valores:** Podem ser strings (ex: `"Gustavo"`), números (ex: `35`), booleanos (ex: `true`), arrays (`[...]`) e outros documentos/objetos (`{...}`).
* **BSON (Binary JSON):** É o formato no qual o MongoDB armazena os registros, contendo uma lista ordenada dos elementos.

## 3. Paradigmas NoSQL

O NoSQL é um paradigma de banco de dados não relacional projetado para oferecer flexibilidade, escalabilidade e alto desempenho. Os quatro principais paradigmas são:

1. **Orientados a documentos:** ex. MongoDB.
2. **Chave-valor:** ex. Redis.
3. **Famílias de colunas (Wide-column):** ex. Cassandra.
4. **Orientados a grafos:** ex. Neo4j.

## 4. Fundamentos do MongoDB

* O nome "Mongo" deriva de *Humongous* (Gigante), projetado para gerenciar grandes volumes de dados de forma eficiente.
* **Schemaless:** Possui uma estrutura sem esquema rígido.
* **Relacionamentos:** Diferente dos bancos relacionais que utilizam JOINs, o MongoDB minimiza o uso de relacionamentos, preferindo armazenar dados relacionados juntos no mesmo documento utilizando documentos incorporados (embedded documents).

## 5. Operações CRUD

Com base nos fundamentos e no mapeamento padrão das operações de banco de dados, as ações principais para manipulação de dados dividem-se em quatro categorias (CRUD):

* **Create (Criar):** 
  * `insertOne(data, options)`
  * `insertMany(data, options)`
* **Read (Ler):** 
  * `find(filter, options)`
  * `findOne(filter, options)`
* **Update (Atualizar):** 
  * `updateOne(filter, data, options)`
  * `updateMany(filter, data, options)`
  * `replaceOne(filter, data, options)`
* **Delete (Deletar):** 
  * `deleteOne(filter, options)`
  * `deleteMany(filter, options)`

## 6. Comandos Principais (Shell)

Comandos para navegação e manipulação via terminal:

* `mongosh`: Inicia o shell.
* `show databases` ou `show dbs`: Mostra os bancos de dados.
* `use <database>`: Troca para o banco de dados especificado.
* `show collections`: Lista as coleções.
* `db.createCollection("<collection_name>")`: Cria uma coleção.
* `db.<collection_name>.insertOne({<object>})`: Insere um documento.
* `db.<collection_name>.find()`: Retorna os documentos da coleção.

## 7. Exemplos Práticos de Aplicação

Abaixo estão alguns exemplos práticos de uso dos comandos shell para gerenciar bancos de dados, coleções e documentos no MongoDB:

**Exibir os bancos de dados:**
```javascript
show databases
```

**Criar ou acessar um banco de dados:**
```javascript
use loja_informatica
```

**Criar uma nova collection:**
```javascript
db.createCollection("cliente")
```

**Mostrar todas as collections do banco atual:**
```javascript
show collections
```

**Inserir apenas 1 document (objeto):**
```javascript
db.cliente.insertOne({
   "nome": "gustavo",
   "idade": 25,
   "pets": ["thor", "pia"],
   "endereco": {
      "logradouro": "parque cajueiro"
   }
})
```

**Inserir muitos documents de uma vez:**
```javascript
db.cliente.insertMany([
   { "nome": "Brenno" },
   { "nome": "João" },
   { "nome": "Maria" },
   { "nome": "José" },
   { "nome": "Noé" }
])
```

**Mostrar todos os documentos/objetos de uma coleção:**
```javascript
db.cliente.find()
```

**Buscar por um campo específico:**
```javascript
db.cliente.find({"nome": "José"})
```

**Buscar pelo identificador único (ObjectId):**
```javascript

## 8. Relacionamentos entre Documentos

No MongoDB, os relacionamentos entre dados podem ser representados principalmente de duas formas:

* **Embarcado (Embedded):** Os dados relacionados são armazenados dentro do mesmo documento.
* **Por referência (Reference):** Os dados relacionados são armazenados em documentos separados e vinculados por meio de um identificador, geralmente utilizando `ObjectId`.

Os principais tipos de relacionamento são:

### 8.1 One-to-One (Um para Um)

Representa uma relação em que um documento possui relação com apenas um outro documento.

#### Embarcado

Os dados relacionados são armazenados diretamente dentro do documento principal:

```javascript
db.patients.insertOne({
   name: "Jefté",
   age: 35,
   diseaseSummary: {
      diseases: ["cold", "broken leg"]
   }
})
```

Nesse exemplo, o resumo das doenças está incorporado ao documento do paciente.

#### Por Referência

Os documentos são armazenados separadamente e relacionados por meio de um `ObjectId`:

```javascript
db.persons.insertOne({
   name: "Jefté",
   age: 35,
   salary: 3000
})

db.cars.insertOne({
   model: "BMW",
   price: 40000,
   owner: ObjectId("6aa9e2cee9c288ce1241317e")
})
```

Nesse caso, o campo `owner` armazena o identificador do documento correspondente à pessoa.

### 8.2 One-to-Many (Um para Muitos)

Representa uma relação em que um documento está associado a vários outros documentos.

#### Embarcado

Os dados relacionados são armazenados como um array dentro do documento principal:

```javascript
db.questionThreads.insertOne({
   creator: "Jefté",
   question: "How does that work?",
   answers: [
      { text: "Like that." },
      { text: "Thanks!" }
   ]
})
```

Nesse exemplo, uma pergunta possui várias respostas armazenadas dentro do próprio documento.

#### Por Referência

Os documentos relacionados são armazenados separadamente e utilizam um identificador para estabelecer a relação:

```javascript
db.cities.insertOne({
   name: "New York City",
   coordinates: {
      lat: 21,
      lng: 55
   }
})

db.citizens.insertMany([
   {
      name: "Jefté Goes",
      cityId: ObjectId("5b98d6b44d01c52e1637a99f")
   },
   {
      name: "Brenno Salvador",
      cityId: ObjectId("5b98d6b44d01c52e1637a99f")
   }
])
```

Nesse exemplo, uma cidade pode estar relacionada a vários cidadãos. O campo `cityId` identifica a cidade à qual cada cidadão pertence.

### 8.3 Many-to-Many (Muitos para Muitos)

Representa uma relação em que vários documentos de uma coleção podem estar relacionados a vários documentos de outra coleção.

#### Embarcado

Os dados relacionados podem ser armazenados dentro do próprio documento, normalmente utilizando arrays:

```javascript
db.customers.insertOne({
   name: "Jefté",
   age: 35
})

db.customers.updateOne(
   {},
   {
      $set: {
         orders: [
            {
               title: "A Book",
               price: 12.99,
               quantity: 2
            }
         ]
      }
   }
)
```

Nesse exemplo, os pedidos são armazenados dentro do documento do cliente.

#### Por Referência

Os documentos são mantidos em coleções diferentes e relacionados por meio de `ObjectId`:

```javascript
db.authors.insertMany([
   {
      name: "Jorge Amado",
      age: 78,
      address: {
         street: "Bahia"
      }
   },
   {
      name: "Graciliano Ramos",
      age: 55,
      address: {
         street: "Rio de Janeiro"
      }
   }
])

db.books.updateOne(
   {},
   {
      $set: {
         authors: [
            ObjectId("5b98d9e44d01c52e1637a9a6"),
            ObjectId("5b98d9e44d01c52e1637a9a7")
         ]
      }
   }
)
```

Nesse caso, um livro pode possuir vários autores, enquanto um autor também pode estar relacionado a vários livros. O relacionamento é estabelecido pelo array `authors`, que armazena os identificadores dos autores.

db.cliente.find({_id: ObjectId('6a7bbab007ff2cf8649f68a9')})
```
