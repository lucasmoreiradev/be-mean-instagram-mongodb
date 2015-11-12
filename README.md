# be-mean-instagram-mongodb 
Guia de referência do conteúdo ministrado no módulo **mongoDB** do curso gratuíto [*Construa seu Instagram com MEAN*](http://dagora.net/be-mean/) da [Webschool.io](https://github.com/Webschool-io/)

## Apresentação (Slides)
[Link para slides](
https://docs.google.com/presentation/d/1KXxmcwd47x4v2SymyiBPK7ucn80PruSvcw4mZ5S3nWc/edit?usp=sharing
)

#### Aula 01 (Export & Import)

*Este resumo da aula 01 foi copiado do repositório do [Vinicius Galvão](https://github.com/viniciusgalvao/be-mean-instagram-mongodb)*

Nessa aula foi falado um pouco sobre o curso [*"Construa seu Instagram com MEAN"*](http://dagora.net/be-mean/) e sua **EMENTA**.

Algumas explicações sobre bancos __NO-SQL__ e seus tipos:
```
- Chave/Valor
- Documentos
- Colunas
- Grafos
```
Foi falado também sobre a *__construção e estrutura__* do __mongoDB__.

Finalizando a aula foram apresentados os comandos `export & import` do __mongoDB__ e uma ferramenta chamada __[mongohacker](https://tylerbrock.github.io/mongo-hacker/)__ que melhora a visualização de buscas e resultados no console.

##### Links da Aula
- [Vídeo da Aula](https://www.youtube.com/watch?v=leYxsEAL_yY)
- [Exercício Solicitado](https://github.com/Webschool-io/be-mean-instagram/blob/master/apostila/mongodb/export_import.md)
- [Exercício Resolvido](https://github.com/Webschool-io/be-mean-instagram/blob/master/apostila/classes/mongodb/exercises/class-01-resolved-viniciusgalvao-vinicius-galvao.md)

================================================

#### Aula 02 (Databases e CRUD)

Nessa aula foi ensinado a criar, listar e escolher databases na qual
queremos trabalhar. Também foi mostrado como podemos criar collections e
lista-las de acordo com a database escolhida. 

Iniciamos os estudos CRUD. Sendo assim, vimos as seguintes funções:
```
- db.pokemons.insert({json}) => (Faz apenas inserção)
- db.pokemons.save({json}) => (Faz inserção ou atualização)
- db.pokemons.find() => (Realiza consulta)
- db.pokemons.findOne() => (Realiza consulta de um objeto específico)
```

#### Links da Aula
- [Vídeo da aula](https://www.youtube.com/watch?v=PaNVk0V2UNI)
- [Exercício Solicitado](https://github.com/Webschool-io/be-mean-instagram/blob/master/apostila/classes/mongodb/class-02-resolved.md)
- [Exercício Resolvido](https://github.com/fauker/be-mean-instagram-mongodb/blob/master/exercises/class-02-resolved-fauker-lucas-moreira.md)

================================================

#### Aula 03 (Busca com Operadores)

A aula foi iniciada com uma breve explicação sobre como o **_id** das
coleções é gerado. Também vimos um pouco sobre a sintaxe da função **find()**,
que é:

```
db.collection.find({query}, {fields})
```

**Query**: É um JSON ```var query = {name: 'Pikachu'}``` que, fazendo
uma analogia com o banco de dados relacional, seria a cláusula
**WHERE**. 

**Fields**: São os campos que nós queremos buscar. Fazendo a mesma
analogia com o banco de dados relacional, os Fields se equivalem ao
**SELECT**. Para isso, deve-se especificar esses campos com 0
(**FALSE**) ou 1 (**TRUE**), da seguinte forma:

```
var query = {name: 'Pikachu'}
var fields = {name: 1, description: 1}
db.pokemons.find(query, fields)
```

O resultado dessa consulta será um documento com apenas o **_id**, que
sempre virá nas consultas, a não ser que a gente o **negue** com o
**false** ```var fields = {_id: 0}```, **nome** e **description**.

Vimos também os **Operadores Aritméticos**. São eles:

Operador | Significado | Equivalência | Forma de uso
-------- | ----------- | ------------ | -----------
$lt | less than (menor que) | < | ```var query = {height: {$lt: 0.5}}``` 
$lte | less than or equal (menor ou igual que) | <= | ```var query = {height: {$lte: 0.5}}```
$gt | greater than (maior que) | > | ```var query = {height: {$gt: 0.5}}``` 
$gte | greater than or equal (maior ou igual que) | >= | `` var query = {height: {$gte: 0.5}}```

Também vimos os **Operadores Lógicos**. Ficam da seguinte forma:

Operador | Significado | Forma de Uso
-------- | ----------- | ------------
$or | OU | ```var query = {$or: [{a: 1}, {b: 2}]}```
$nor | Not OU | ```var query = {$nor: [{a: 1}, {b: 2}]}```
$and | E | ```var query = {$and: [{a: 1}, {b: 5}]}```

Também vimos no final, mas não menos importante, os **Operadores
Existenciais**:

Operador | Significado | Forma de Uso
-------- | ----------- | ------------
$exists | Existe | ```var query = {campo: {$exists: true}}``` 

#### Links da Aula
- [Vídeo da aula](https://www.youtube.com/watch?v=cIHjA1hyPPY)
- [Exercício Solicitado](https://github.com/Webschool-io/be-mean-instagram/blob/master/apostila/classes/mongodb/class-03-resolved.md)
- [Exercício Resolvido](https://github.com/fauker/be-mean-instagram-mongodb/blob/master/exercises/class-03-resolved-fauker-lucas-moreira.md)
