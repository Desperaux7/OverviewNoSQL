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

As operações principais para manipulação de dados são:

* **Create:** `insertOne(data, options)`.
* **Read:** `find(filter, options)` e `findOne(filter, options)`.
* **Update:** `updateOne(filter, data, options)`, `updateMany(filter, data, options)` e `replaceOne(filter, data, options)`.
* **Delete:** `deleteOne(filter, options)` e `deleteMany(filter, options)`.

## 6. Comandos Principais (Shell)

Comandos para navegação e manipulação via terminal:

* `mongosh`: Inicia o shell.
* `show databases` / `show dbs`: Mostra os bancos de dados.
* `use <database>`: Troca para o banco de dados especificado.
* `show collections`: Lista as coleções.
* `db.createCollection("<collection_name>")`: Cria uma coleção.
* `db.<collection_name>.insertOne({<object>})`: Insere um documento.
* `db.<collection_name>.find()`: Retorna os documentos da coleção.
