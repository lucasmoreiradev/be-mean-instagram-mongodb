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

### Aula 03 (Busca com Operadores)

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
analogia com o banco de dados relacional, os Fields são equivalentes  ao
**SELECT**. Para isso, deve-se especificar esses campos com 0
(**FALSE**) ou 1 (**TRUE**), da seguinte forma:

```
var query = {name: 'Pikachu'}
var fields = {name: 1, description: 1}
db.pokemons.find(query, fields)
```

Resultado:

```
{
  "_id": ObjectId("5642723a76cb4bb0ef93cbb8"),
  "name": "Pikachu",
  "description": "Rato elétrico bem fofinho"
}
```

O resultado possui um documento com **_id**, **name** e
**description**. Mas, ***_id***???? Sim! Ele sempre virá nas consultas,
a não ser que ele seja **negado**! ```var fields = {_id: 0}```

Vimos também os **Operadores Aritméticos**. São eles:

Operador | Significado | Equivalência | Forma de uso
-------- | ----------- | ------------ | -----------
$lt | less than (menor que) | < | ```var query = {height: {$lt: 0.5}}``` 
$lte | less than or equal (menor ou igual que) | <= | ```var query = {height: {$lte: 0.5}}```
$gt | greater than (maior que) | > | ```var query = {height: {$gt: 0.5}}``` 
$gte | greater than or equal (maior ou igual que) | >= | ```var query = {height: {$gte: 0.5}}```

Também vimos os **Operadores Lógicos**. Ficam da seguinte forma:

Operador | Significado | Forma de Uso
-------- | ----------- | ------------
$or | OU | ```var query = {$or: [{a: 1}, {b: 2}]}```
$nor | Not OU | ```var query = {$nor: [{a: 1}, {b: 2}]}```
$and | E | ```var query = {$and: [{a: 1}, {b: 5}]}```

E por fim, vimos os **Operadores Existenciais**:

Operador | Significado | Forma de Uso
-------- | ----------- | ------------
$exists | Existe | ```var query = {campo: {$exists: true}}``` 

##### Links da Aula
- [Vídeo da aula](https://www.youtube.com/watch?v=cIHjA1hyPPY)
- [Exercício Solicitado](https://github.com/Webschool-io/be-mean-instagram/blob/master/apostila/classes/mongodb/class-03-resolved.md)
- [Exercício Resolvido](https://github.com/fauker/be-mean-instagram-mongodb/blob/master/exercises/class-03-resolved-fauker-lucas-moreira.md)

================================================

#### Aula 04 (Função updade)

#### Parte 1 

A aula foi iniciada mostrando que temos duas formas de alterar um
documento. São elas:

- save
- update

Ambos podem fazer atualizações no documento, porém, com o **save** precisamos
recuperar o documento para depois efetuar as alterações. Com o
**update** isso não é necessário. Podemos alterar diretamente.

A função **update** recebe 3 parâmetros: 

- query
- modificação
- options

E tem por sintaxe:

```
db.collection.update(query, modifications, options);
```

***Atenção: não passar as modifications diretamente em uma variável para
a função update, pois ele pode sumir com os outros campos do
documento. Para efetuar um update da forma correta, existem os
operadores de modificação***. 

#### Operadores de modificação

**$set**: modifica ou cria um valor, caso ele não exista. Sintaxe:
`{$set: {campo: valor}}`. Exemplo: 

```
db.pokemons.update({name: 'Pikachu'}, {$set: {attack: 120}})
```

Caso o campo `attack` já exista no documento, este campo será
atualizado. Caso não exista, ele será criado com o valor de **120**.

**$unset**: Tem a mesma sintaxe que o `$set`, porém ele é utilizado para
remover campos. Exemplo:

```
db.pokemons.update({name: 'Pikachu'}, {$unset: {height: 1}})
```

**$inc**: incrementa um valor no campo com a quantidade informada. Caso
o campo não exista, ele irá criar o campo e setar o valor.

***Obs: Para DECREMENTAR, basta passar o valor NEGATIVO***.

Sintaxe: `{$inc: {campo: valor}}`

Para incrementar: `db.pokemons.update({name: 'Pikachu'}, {$inc:
{attack: 10}})`

Para decrementar: `db.pokemons.update({name: 'Pikachu'}, {$inc: {attack: -10}})`

##### Operadores de Array

##### $push

O operador `$push` adiciona um valor ao campo. Caso o campo seja um
array existente, ele irá adicionar valores. Caso o campo não exista, ele
será criado.

Sintaxe: `{$push: {campo: valor}}`

##### $pushAll

É passado um array de valores para um campo no documento. Eles devem ser
adicionados um a um. Caso o
array não exista no documento, ele será criado.

Sintaxe: `{$pushAll: {campo: [valores]}}`

##### $pull

Remove um determinado valor de um array existente. Caso o array não
exista, o comando será ignorado.

Sintaxe: `{$pull: {campo: valor}}`

##### $pullAll

É passado um array de valores para um campo no documento. Eles devem ser
removidos um a um. Caso o array não exista no documento, ele será
ignorado.

Sintaxe: `{$pullAll: {campo: [valores]}}`

Obs: em todos os casos dos **Operadores de Array** se o campo existir e
não for um array, irá retornar um erro.

##### Links da Aula
- [Vídeo da aula](https://www.youtube.com/watch?v=ONzJsNbv15U)

#### Parte 2

O Suissa disse que a [documentação do
MongoDB](https://docs.mongodb.org/manual) é muito simples e bem
explicada.

Na parte 01 dessa aula 04 vimos que a sintaxe da função **update** é:
`db.collection.update(query, modifications, options)`. Bom, na primeira
parte da aula, trabalhamos bem utilizando somente os dois primeiros
parâmetros. Já na segunda parte da aula, vimos o objeto **options**, que
serve para configurarmos alguns valores diferentes do padrão para o
**update**.

Sintaxe: 

```
{
  upsert:boolean,
  multi: boolean,
  writeConcern: document
}
```

##### upsert

Serve para caso o documento não seja encontrado pela **query**, ele
insira o objeto que está sendo passado como modificação.

Defaul: **FALSE**.

##### setOnInsert

Com esse operador podemos definir valores que serão adicionados apenas
se ocorrer um **upsert**, ou seja, se o objeto for inserido quando não
for achado pela **query**. Exemplo:

```
var query = {name: /NaoExisteMon/i}
var mod = {
  $setOnInsert: {
    name: 'NaoExisteMon',
    attack: null,
    defense: null,
    height: null,
    description: 'Sem maiores informações'
  }
}
var options = {upsert: true}
db.pokemons.update(query, mod, options)
```

##### multi

Se não 'setarmos' o operador **multi** como ***TRUE***, não podemos dar
um update em mais de um documento. Exemplo de sintaxe:

```
var query = {}
var mod = {$set: {active: false}}
var options = {multi: true}
db.pokemons.update(query, mod, options)
```

Esse update será feito em TODOS os documentos, porque o operador
**MULTI** está como verdadeiro.

Voltamos às buscas. Função find. Precisamos saber alguns operadores de
array para buscamos documentos mais precisamente. 

##### função find() - operadores de array

**$in**: O operador **$in** retorna os documentos que possuem algum dos
valores passados no array. Sintaxe: `{campo: {$in: [Array]}`.

**$nin**: O contrário do **$in**, mesma sintaxe.

**$all**: Retorna documentos que possuem todos os valores informados no
array. Mesma sintaxe dos operadores anteriores.

###### Operadore de Negação

**$ne**: not Equal. Não funciona com regex. Sintaxe: `{campo: {$ne:
valor}}`.

**$not**: (Operador Lógico de Negação) funciona com regex ou com
documentos. Sintaxe: `{campo: {$not: valor}}`.

##### remove

Para apagar dados de uma coleção, usaremos o **remove**.

Obs: ele apenas apaga os dados, porém a coleção continua existindo. Para
apagar a coleção, deve-se utilizar a função **drop()**.

##### Links da Aula
- [Vídeo da aula](https://www.youtube.com/watch?v=ozbmQb6SVQk)
- [Exercício Solicitado](https://github.com/Webschool-io/be-mean-instagram/blob/master/apostila/classes/mongodb/class-04-resolved.md)
- [Exercício Resolvido](https://github.com/fauker/be-mean-instagram-mongodb/blob/master/exercises/class-04-resolved-fauker-lucas-moreira.md)

================================================

#### Aula 05 

Dicas: 

- É bom sempre dar um findOne() para conhecer o objeto e a estrutura da
database.

- Caso não esteja utilizando o mongohack, para identar os resultados do mongo basta chamar a função **pretty()**.

##### count

A aula foi inicada mostrando um pouco sobre a função **count()**, vimos que a performance de utilizá-lo ao invés de utilizar o **find().lenght** para contar os registros é imensamente maior. A função **count()** também aceita querys por parâmetro. `count({})`.

##### distinct

A função **distinct()** tem a mesma ideia do **distinct** do SQL: não trazer dados
repetidos. 

Sintaxe: `db.resturantes.distinct('borough')`.

Ele retorna um array; podemos pegar diretamente esse array e coloca-lo em ordem
alfabética dando um `db.restaurantes.distinct('borough').sort()`. Caso seja necessário inverter a ordem de A-Z para Z-A, basta colocar um **reverse()** depois do **sort()**.

##### importação / exportação

Relembramos como importare e exportar coleções para o MondoDB.

para exportar uma collection: 

```
mongoexport --host 127.0.0.1 --db
-nome-database --collection nome-collection --out saida.json
```

para importar uma coleção:

```
mongoimport --host 127.0.0.1 --db -nome-database --collections
nome-colecao --drop --file entrada.json
```

##### limit

Serve para limitarmos a quantidade de coleções que teremos como resultado em uma busca. Por exemplo:

`limit - find(query, campos).limit(quantidadeDeDadosQueEuPedir)`


##### skip

Serve para pula registros. É resultado de uma multiplicacao. Por exemplo: se
precisarmos paginar de 10 em 10, teremos de fazer o seguinte:

```
db.pokemons.find({}, {name: 1, _id: 0}.limit(10).skip(10 * 0)

0, no caso, é a página. (primeira página)
```

##### group

Simplesmente agrupa alguma coisa.

`//TODO exemplo`

##### agregate

Agrupa documentos também. Basicamente tudo o que fazemos com o **group()**, podemos fazer com o **agregate()**.

`//TODO exemplo`


##### Links da Aula
- [Vídeo da aula](https://www.youtube.com/watch?v=1eHc8reT_Vk)
- Exercício Solicitado (ainda não achei o link)
- [Exercício Resolvido](https://github.com/fauker/be-mean-instagram-mongodb/blob/master/exercises/class-05-resolved-fauker-lucas-moreira.md)

================================================
