# MongoDb - Projeto Final
**Autor:** Lucas da Silva Moreira

**Data** Date.now() //em timestamp

## Para qual sistema você usaria o MogoDB (diferente desse)?
- Chat
- ERP
- Sistemas de CRUD
- Sistemas que eu tenha que mostrar várias informações de uma vez

## Qual a modelagem da sua coleção de `users`?

```
user: {
	id_user: ObjectId,
	name: String,
	bio: String,
	date_register: Date,
	avatar_path: String,
	background_path: String,

	auth: {
		username: String,
		email: String,
		password: String,
		last_acess: Date,
		online: Boolean,
		disabled: Boolean,
		hash-token: String
	}
}
```

## Qual a modelagem da sua coleção de `projects`?

```
project: {
	id_project: ObjectId,
	name: String,
	description: String,
	date_begin: String,
	date_dream: String,
	date_end: String,
	visible: Boolean,
	realocate: Boolean,
	expired: Boolean,
	visualizable_mod: String,
	tags: [
		{
			tag_id: ObjectId
		}
	],

	goals: [
		{
			name: String,
			description: String,
			date_begin: Date,
			date_dream: Date,
			date_end: Date,
			realocate: Boolean,
			expired: Boolean,
			tags: [
				{
					tag_id: ObjectId
				}
			],			

			historic: {
				date_realocate: Date
			},
			activities: [
				{ 
					activity_id: ObjectId 
				}
			]			
		}
	],

	members: [
		{
			id_user: ObjectId,
			notify: String,
			type: String,

			activities: [
				{
					activity_id: ObjectId,
				}
			],

			comments: [
				{
		            text: String,
		            date_comment: String,
		            files: [
		            	{
		            		path: String,
		            		weight: String,
		            		name: String
		            	}
		            ]					
				}
			]
		}
}

```

## Qual a modelagem da sua coleção retirada de `projects`?

```
activity: {
	name: String,
	description: String,
	date_begin: Date,
	date_dream: Date,
	date_end: Date,
	realocate: Boolean,
	expired: Boolean,

	historic: {
		date_realocate: Date
	},

	tags: [
		{		
			tag_id: ObjectId
		}
	],	

	members: [
		{
			id_user: ObjectId,
			notify: String,
			type: String,

			comments: [
				{
		            text: String,
		            date_comment: String,
		            files: [
		            	{
		            		path: String,
		            		weight: String,
		            		name: String
		            	}
		            ]					
				}
			]

		}
	],
}
```

## Create - cadastro

#### 1. Cadastre 10 usuários diferentes.

```
var users = [
	{name: "Adriana Castelhano", username: "adriana_castelhado"},
	{name: "Cleusa Antas", username: "cleusa_antas"},
	{name: "Eusébio Piñero", username: "eusebio_pinero"},
	{name: "Ilma Doutel", username: "ilma_doutel"},
	{name: "Marina Carvalhosa", username: "marina_carvalhosa"},
	{name: "Milena Nieves", username: "milena_nieves"},
	{name: "Nádia Santos", username: "nadia_santos"},
	{name: "Palo Tamoio", username: "palo_tamoio"},
	{name: "Silvana Jordão", username: "silvana_jordao"},
	{name: "Virgínia Remígio", username: "virginia_remigio"}	
]

var usersList = []

users.forEach(function(user) {
	var query = {
		name: user.name,
		bio: "Lifelong communicator. Pop culture buff. Beer expert. Proud zombie practitioner.",
		date_register: new Date(),
		avatar_path: "http://i2.wp.com/tecnodia.com.br/wp-content/uploads/2013/05/facebook-geek-avatar.jpg",
		background_path: "http://www.pulsarwallpapers.com/data/media/3/Alien%20Ink%202560X1600%20Abstract%20Background.jpg",
		auth: {
			username: user.username,
			email: user.username+"@email.com",
			password: user.username+"@"+user.username.length,
			last_acess: new Date(),
			online: true,
			disabled: false,
			hash_token: "698dc19d489c4e4db73e28a713eab07b"+user.username.length
		}
	}
	usersList.push(query)
})

db.users.insert(usersList)

Inserted 1 record(s) in 553ms
BulkWriteResult({
  "writeErrors": [ ],
  "writeConcernErrors": [ ],
  "nInserted": 10,
  "nUpserted": 0,
  "nMatched": 0,
  "nModified": 0,
  "nRemoved": 0,
  "upserted": [ ]
})
```

## Retrieve - busca

## Update - alteração

## Delete - remoção

## Sharding
// coloque aqui todos os comandos que você executou

## Replica
// coloque aqui todos os comandos que você executou
