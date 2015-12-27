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
	date-register: Date,
	avatar-path: String,
	background-path: String,

	auth: {
		username: String,
		email: String,
		password: String,
		last-acess: Date,
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

## Retrieve - busca

## Update - alteração

## Delete - remoção

## Sharding
// coloque aqui todos os comandos que você executou

## Replica
// coloque aqui todos os comandos que você executou
