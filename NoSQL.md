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
   "nome": "jefté",
   "idade": 35,
   "pets": ["dora", "sabrina"],
   "endereco": {
      "logradouro": "Sossego"
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
db.cliente.find({_id: ObjectId('6a7bbab007ff2cf8649f68a9')})
```
