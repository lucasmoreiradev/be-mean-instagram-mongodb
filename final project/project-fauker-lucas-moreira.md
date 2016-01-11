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
  "id": ObjectId
  "name": String
  "description": String
  "date_begin": Date(),
  "date_dream": Date(),
  "date_end": Date(),
  "visible": boolean
  "realocate": boolean,
  "expired": boolean,
  "visualizable_mod": String
  "tags": [],
  "goals": [
    {
      "name": String
      "description": String,
      "date_begin": Date(),
      "date_dream": Date(),
      "date_end": Date(),
      "realocate": boolean
      "expired": boolean
      "tags": [],
      "historic": {
        "date_realocate": Date()
      },
      "activities": [
        {
          "activity_id": ObjectId
        }
      ]
    }
  ],
  "members": [
    {
      "id_user": ObjectId,
      "notify": String
      "type": String
    }
  ]
}
```

## Qual a modelagem da sua coleção retirada de `projects`?

```
activity: {
	name: String
	description: String
	date_begin: Date(),
	date_dream: Date(),
	date_end: Date(),
	realocate: false,
	expired: false,

	historic: {
		date_realocate: Date()
	},

	tags: [],

	members: [{
		id_user: ObjectId,
		notify: String,
		type: String,
	}],

	comments: [{
		members: [{
			id_user: ObjectId,
			notify: String,
			type: String,
		}],
        text: String,
        date_comment: Date(),
        files: [{
			path: String,
			weight: String,
			name: String
		}]				
	}]
}
```

TODO: explicação

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

#### 2. Cadastre 5 projetos diferentes.
- cada um com 5 membros, sempre diferentes dentro dos projetos;
- cada um com pelo menos 3 tags diferentes;
    - escolha 1 *tag* onde deva ficar em 2 projetos;
    - escolha 1 *tag* onde deva ficar em 3 projetos;
- cada projeto com pelo menos 1 *goal*;
    - cada *goal* com pelo menos 3 *tags*;
    - cada *goal* com pelo menos 2 atividades, deixe 1 projeto sem.

```

// Salvando duas atividades para referenciar nos projetos

for (var i = 1; i <= 2; i++) {
	db.activities.insert({ 
		name: 'Atividade número ' + i,
		description: 'Descrição da atividade número ' + i,
		date_begin: new Date(),
		date_dream: new Date(),
		date_end: new Date(),
		realocate: false,
		expired: false,
		historic: {
			date_realocate: new Date()
		},
		tags: [],
		members: [],
		comments: []
	})
}
Inserted 1 record(s) in 555ms
Inserted 1 record(s) in 2ms
WriteResult({
  "nInserted": 1
})
Atividade número 1: "_id": ObjectId("5689a2fbc3f8dbd6487e1c74"),
Atividade número 2: "_id": ObjectId("5689a2fcc3f8dbd6487e1c75"),

var users = db.users.find({}, {id: 1}).toArray()

db.projects.insert([
{
  "name": "Primeiro projeto",
  "description": "Meu primeiro projeto",
  "date_begin": new Date(),
  "date_dream": new Date(),
  "date_end": new Date(),
  "visible": true,
  "realocate": true,
  "expired": false,
  "visualizable_mod": "asopijovjsaopivjasdoivj",
  "tags": [
    "Suissa",
    "Be MEAN",
    "MongoDB"
  ],
  "goals": [
    {
      "name": "Ficar mt loco nas programações",
      "description": "Ce não tá ligado",
      "date_begin": new Date(),
      "date_dream": new Date(),
      "date_end": new Date(),
      "realocate": false,
      "expired": false,
      "tags": [
        "JavaScript",
        "Programação",
        "Code"
      ],
      "historic": {
        "date_realocate": new Date(),
      },
      "activities": [
        {
          "activity_id": ObjectId("5689a2fbc3f8dbd6487e1c74")
        },
        {
          "activity_id": ObjectId("5689a2fcc3f8dbd6487e1c75")
        }
      ]
    }
  ],
  "members": [
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc6"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc7"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc8"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc9"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afca"),
      "notify": "Notificação",
      "type": "Membro"
    }
  ]
},
{
  "name": "segunro projeto",
  "description": "Meu segunro projeto",
  "date_begin": new Date(),
  "date_dream": new Date(),
  "date_end": new Date(),
  "visible": true,
  "realocate": true,
  "expired": false,
  "visualizable_mod": "asopijovjsaopivjasdoivj",
  "tags": [
    "Suissa",
    "Be MEAN",
    "JavaScript"
  ],
  "goals": [
    {
      "name": "Ficar expert",
      "description": "Sé doido manuuuuu",
      "date_begin": new Date(),
      "date_dream": new Date(),
      "date_end": new Date(),
      "realocate": false,
      "expired": false,
      "tags": [
        "JavaScript",
        "Programação",
        "Code"
      ],
      "historic": {
        "date_realocate": new Date(),
      },
      "activities": [
        {
          "activity_id": ObjectId("5689a2fbc3f8dbd6487e1c74")
        },
        {
          "activity_id": ObjectId("5689a2fcc3f8dbd6487e1c75")
        }
      ]
    }
  ],
  "members": [
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc6"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc7"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc8"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc9"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afca"),
      "notify": "Notificação",
      "type": "Membro"
    }
  ]
},
{
  "name": "terceiro projeto",
  "description": "Meu terceiro projeto",
  "date_begin": new Date(),
  "date_dream": new Date(),
  "date_end": new Date(),
  "visible": true,
  "realocate": true,
  "expired": false,
  "visualizable_mod": "asopijovjsaopivjasdoivj",
  "tags": [
    "Webschool",
    "Be MEAN",
    "Web"
  ],
  "goals": [
    {
      "name": "Entender mais a stack MEAN",
      "description": "MEAN NA VEIA!!!!",
      "date_begin": new Date(),
      "date_dream": new Date(),
      "date_end": new Date(),
      "realocate": false,
      "expired": false,
      "tags": [
        "JavaScript",
        "Programação",
        "Code"
      ],
      "historic": {
        "date_realocate": new Date(),
      },
      "activities": [
        {
          "activity_id": ObjectId("5689a2fbc3f8dbd6487e1c74")
        },
        {
          "activity_id": ObjectId("5689a2fcc3f8dbd6487e1c75")
        }
      ]
    }
  ],
  "members": [
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc6"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc7"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc8"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc9"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afca"),
      "notify": "Notificação",
      "type": "Membro"
    }
  ]
},
{
  "name": "quarto projeto",
  "description": "Meu Quarto projeto",
  "date_begin": new Date(),
  "date_dream": new Date(),
  "date_end": new Date(),
  "visible": true,
  "realocate": true,
  "expired": false,
  "visualizable_mod": "asopijovjsaopivjasdoivj",
  "tags": [
    "Frontend",
    "Workshop",
    "http"
  ],
  "goals": [
    {
      "name": "desenvolver tudo com JSS",
      "description": "PQ JS EH TOPPPPP",
      "date_begin": new Date(),
      "date_dream": new Date(),
      "date_end": new Date(),
      "realocate": false,
      "expired": false,
      "tags": [
        "JavaScript",
        "Programação",
        "Code"
      ],
      "historic": {
        "date_realocate": new Date(),
      },
      "activities": [
        {
          "activity_id": ObjectId("5689a2fbc3f8dbd6487e1c74")
        },
        {
          "activity_id": ObjectId("5689a2fcc3f8dbd6487e1c75")
        }
      ]
    }
  ],
  "members": [
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc6"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc7"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc8"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc9"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afca"),
      "notify": "Notificação",
      "type": "Membro"
    }
  ]
},
{
  "name": "quintoProjeto projeto",
  "description": "Meu Quinto projeto",
  "date_begin": new Date(),
  "date_dream": new Date(),
  "date_end": new Date(),
  "visible": true,
  "realocate": true,
  "expired": false,
  "visualizable_mod": "asopijovjsaopivjasdoivj",
  "tags": [
    "js",
    "mean",
    "stack"
  ],
  "goals": [
    {
      "name": "ficar fodassalhao em js",
      "description": "tudo agora será em js",
      "date_begin": new Date(),
      "date_dream": new Date(),
      "date_end": new Date(),
      "realocate": false,
      "expired": false,
      "tags": [
        "JavaScript",
        "Programação",
        "Code"
      ],
      "historic": {
        "date_realocate": new Date(),
      },
      "activities": [ ]
    }
  ],
  "members": [
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc6"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc7"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc8"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc9"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afca"),
      "notify": "Notificação",
      "type": "Membro"
    }
  ]
}])

Inserted 1 record(s) in 517ms
BulkWriteResult({
  "writeErrors": [ ],
  "writeConcernErrors": [ ],
  "nInserted": 5,
  "nUpserted": 0,
  "nMatched": 0,
  "nModified": 0,
  "nRemoved": 0,
  "upserted": [ ]
})

```

## Retrieve - busca

#### 1. Liste as informações dos membros de 1 projeto específico que deve ser buscado pelo seu nome de forma a não ligar para maiúsculas e minúsculas.

```
var query = {name: /primeiro projeto/i}
var fields = {_id: 0, members: 1}
var membrosDosProjetos = db.projects.findOne(query, fields)

var membros = [];

membrosDosProjetos.members.forEach(function(membro) {
	membros.push(db.users.findOne({_id: membro.id_user}))	
})

membros

[
  {
    "_id": ObjectId("56807d83e15bcf96ff94afc6"),
    "name": "Cleusa Antas",
    "bio": "Lifelong communicator. Pop culture buff. Beer expert. Proud zombie practitioner.",
    "date_register": ISODate("2015-12-28T00:08:29.811Z"),
    "avatar_path": "http://i2.wp.com/tecnodia.com.br/wp-content/uploads/2013/05/facebook-geek-avatar.jpg",
    "background_path": "http://www.pulsarwallpapers.com/data/media/3/Alien%20Ink%202560X1600%20Abstract%20Background.jpg",
    "auth": {
      "username": "cleusa_antas",
      "email": "cleusa_antas@email.com",
      "password": "cleusa_antas@12",
      "last_acess": ISODate("2015-12-28T00:08:29.811Z"),
      "online": true,
      "disabled": false,
      "hash_token": "698dc19d489c4e4db73e28a713eab07b12"
    }
  },
  {
    "_id": ObjectId("56807d83e15bcf96ff94afc7"),
    "name": "Eusébio Piñero",
    "bio": "Lifelong communicator. Pop culture buff. Beer expert. Proud zombie practitioner.",
    "date_register": ISODate("2015-12-28T00:08:29.811Z"),
    "avatar_path": "http://i2.wp.com/tecnodia.com.br/wp-content/uploads/2013/05/facebook-geek-avatar.jpg",
    "background_path": "http://www.pulsarwallpapers.com/data/media/3/Alien%20Ink%202560X1600%20Abstract%20Background.jpg",
    "auth": {
      "username": "eusebio_pinero",
      "email": "eusebio_pinero@email.com",
      "password": "eusebio_pinero@14",
      "last_acess": ISODate("2015-12-28T00:08:29.811Z"),
      "online": true,
      "disabled": false,
      "hash_token": "698dc19d489c4e4db73e28a713eab07b14"
    }
  },
  {
    "_id": ObjectId("56807d83e15bcf96ff94afc8"),
    "name": "Ilma Doutel",
    "bio": "Lifelong communicator. Pop culture buff. Beer expert. Proud zombie practitioner.",
    "date_register": ISODate("2015-12-28T00:08:29.811Z"),
    "avatar_path": "http://i2.wp.com/tecnodia.com.br/wp-content/uploads/2013/05/facebook-geek-avatar.jpg",
    "background_path": "http://www.pulsarwallpapers.com/data/media/3/Alien%20Ink%202560X1600%20Abstract%20Background.jpg",
    "auth": {
      "username": "ilma_doutel",
      "email": "ilma_doutel@email.com",
      "password": "ilma_doutel@11",
      "last_acess": ISODate("2015-12-28T00:08:29.811Z"),
      "online": true,
      "disabled": false,
      "hash_token": "698dc19d489c4e4db73e28a713eab07b11"
    }
  },
  {
    "_id": ObjectId("56807d83e15bcf96ff94afc9"),
    "name": "Marina Carvalhosa",
    "bio": "Lifelong communicator. Pop culture buff. Beer expert. Proud zombie practitioner.",
    "date_register": ISODate("2015-12-28T00:08:29.811Z"),
    "avatar_path": "http://i2.wp.com/tecnodia.com.br/wp-content/uploads/2013/05/facebook-geek-avatar.jpg",
    "background_path": "http://www.pulsarwallpapers.com/data/media/3/Alien%20Ink%202560X1600%20Abstract%20Background.jpg",
    "auth": {
      "username": "marina_carvalhosa",
      "email": "marina_carvalhosa@email.com",
      "password": "marina_carvalhosa@17",
      "last_acess": ISODate("2015-12-28T00:08:29.811Z"),
      "online": true,
      "disabled": false,
      "hash_token": "698dc19d489c4e4db73e28a713eab07b17"
    }
  },
  {
    "_id": ObjectId("56807d83e15bcf96ff94afca"),
    "name": "Milena Nieves",
    "bio": "Lifelong communicator. Pop culture buff. Beer expert. Proud zombie practitioner.",
    "date_register": ISODate("2015-12-28T00:08:29.811Z"),
    "avatar_path": "http://i2.wp.com/tecnodia.com.br/wp-content/uploads/2013/05/facebook-geek-avatar.jpg",
    "background_path": "http://www.pulsarwallpapers.com/data/media/3/Alien%20Ink%202560X1600%20Abstract%20Background.jpg",
    "auth": {
      "username": "milena_nieves",
      "email": "milena_nieves@email.com",
      "password": "milena_nieves@13",
      "last_acess": ISODate("2015-12-28T00:08:29.811Z"),
      "online": true,
      "disabled": false,
      "hash_token": "698dc19d489c4e4db73e28a713eab07b13"
    }
  }
]
```

#### 2. Liste todos os projetos com a tag que você escolheu para os 3 projetos em comum.

A tag que eu escolhi para inserir em 3 projetos foi **Be MEAN**!!!

```
var query = {tags: {$in: ['Be MEAN']}}
db.projects.find(query)
{
  "_id": ObjectId("568c0576c3f8dbd6487e1c89"),
  "name": "Primeiro projeto",
  "description": "Meu primeiro projeto",
  "date_begin": ISODate("2016-01-05T18:03:34.041Z"),
  "date_dream": ISODate("2016-01-05T18:03:34.041Z"),
  "date_end": ISODate("2016-01-05T18:03:34.041Z"),
  "visible": true,
  "realocate": true,
  "expired": false,
  "visualizable_mod": "asopijovjsaopivjasdoivj",
  "tags": [
    "Suissa",
    "Be MEAN",
    "MongoDB"
  ],
  "goals": [
    {
      "name": "Ficar mt loco nas programações",
      "description": "Ce não tá ligado",
      "date_begin": ISODate("2016-01-05T18:03:34.041Z"),
      "date_dream": ISODate("2016-01-05T18:03:34.041Z"),
      "date_end": ISODate("2016-01-05T18:03:34.041Z"),
      "realocate": false,
      "expired": false,
      "tags": [
        "JavaScript",
        "Programação",
        "Code"
      ],
      "historic": {
        "date_realocate": ISODate("2016-01-05T18:03:34.042Z")
      },
      "activities": [
        {
          "activity_id": ObjectId("5689a2fcc3f8dbd6487e1c74")
        },
        {
          "activity_id": ObjectId("5689a2fcc3f8dbd6487e1c75")
        }
      ]
    }
  ],
  "members": [
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc6"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc7"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc8"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc9"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afca"),
      "notify": "Notificação",
      "type": "Membro"
    }
  ]
}
{
  "_id": ObjectId("568c0576c3f8dbd6487e1c8a"),
  "name": "segunro projeto",
  "description": "Meu segunro projeto",
  "date_begin": ISODate("2016-01-05T18:03:34.092Z"),
  "date_dream": ISODate("2016-01-05T18:03:34.092Z"),
  "date_end": ISODate("2016-01-05T18:03:34.092Z"),
  "visible": true,
  "realocate": true,
  "expired": false,
  "visualizable_mod": "asopijovjsaopivjasdoivj",
  "tags": [
    "Suissa",
    "Be MEAN",
    "JavaScript"
  ],
  "goals": [
    {
      "name": "Ficar expert",
      "description": "Sé doido manuuuuu",
      "date_begin": ISODate("2016-01-05T18:03:34.092Z"),
      "date_dream": ISODate("2016-01-05T18:03:34.092Z"),
      "date_end": ISODate("2016-01-05T18:03:34.092Z"),
      "realocate": false,
      "expired": false,
      "tags": [
        "JavaScript",
        "Programação",
        "Code"
      ],
      "historic": {
        "date_realocate": ISODate("2016-01-05T18:03:34.092Z")
      },
      "activities": [
        {
          "activity_id": ObjectId("5689a2fcc3f8dbd6487e1c74")
        },
        {
          "activity_id": ObjectId("5689a2fcc3f8dbd6487e1c75")
        }
      ]
    }
  ],
  "members": [
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc6"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc7"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc8"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc9"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afca"),
      "notify": "Notificação",
      "type": "Membro"
    }
  ]
}
{
  "_id": ObjectId("568c0576c3f8dbd6487e1c8b"),
  "name": "terceiro projeto",
  "description": "Meu terceiro projeto",
  "date_begin": ISODate("2016-01-05T18:03:34.092Z"),
  "date_dream": ISODate("2016-01-05T18:03:34.092Z"),
  "date_end": ISODate("2016-01-05T18:03:34.092Z"),
  "visible": true,
  "realocate": true,
  "expired": false,
  "visualizable_mod": "asopijovjsaopivjasdoivj",
  "tags": [
    "Webschool",
    "Be MEAN",
    "Web"
  ],
  "goals": [
    {
      "name": "Entender mais a stack MEAN",
      "description": "MEAN NA VEIA!!!!",
      "date_begin": ISODate("2016-01-05T18:03:34.092Z"),
      "date_dream": ISODate("2016-01-05T18:03:34.092Z"),
      "date_end": ISODate("2016-01-05T18:03:34.092Z"),
      "realocate": false,
      "expired": false,
      "tags": [
        "JavaScript",
        "Programação",
        "Code"
      ],
      "historic": {
        "date_realocate": ISODate("2016-01-05T18:03:34.092Z")
      },
      "activities": [
        {
          "activity_id": ObjectId("5689a2fcc3f8dbd6487e1c74")
        },
        {
          "activity_id": ObjectId("5689a2fcc3f8dbd6487e1c75")
        }
      ]
    }
  ],
  "members": [
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc6"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc7"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc8"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afc9"),
      "notify": "Notificação",
      "type": "Membro"
    },
    {
      "id_user": ObjectId("56807d83e15bcf96ff94afca"),
      "notify": "Notificação",
      "type": "Membro"
    }
  ]
}
```

#### 3. Liste apenas os nomes de todas as atividades para todos os projetos.

```
var nomesAtividades = []
var projetos = db.projects.find({}, {'goals.activities': 1, _id: 0}).toArray()
  projetos.forEach(function (projeto) {
    var atividades = projeto.goals[0].activities
    atividades.forEach(function (atividade) {
      var atv = db.activities.findOne({_id: atividade.activity_id})
      if (atv) {
          nomesAtividades.push(atv.name)
      }
    })
  })

nomesAtividades
[
  "Atividade número 1",
  "Atividade número 2",
  "Atividade número 1",
  "Atividade número 2",
  "Atividade número 1",
  "Atividade número 2",
  "Atividade número 1",
  "Atividade número 2"
]
```

#### 4. Liste todos os projetos que não possuam uma tag.

```
var query = { tags:  { $not: { $in: ['JavaScript'] } } }
db.projects.find(query, {name: 1})
{
  "_id": ObjectId("568c0576c3f8dbd6487e1c89"),
  "name": "Primeiro projeto"
}
{
  "_id": ObjectId("568c0576c3f8dbd6487e1c8b"),
  "name": "terceiro projeto"
}
{
  "_id": ObjectId("568c0576c3f8dbd6487e1c8c"),
  "name": "quarto projeto"
}
{
  "_id": ObjectId("568c0576c3f8dbd6487e1c8d"),
  "name": "quintoProjeto projeto"
}
```

#### 5. Liste todos os usuários que não fazem parte do primeiro projeto cadastrado.

```
var usuariosPrimeiroProjeto = db.projects.findOne({name: /primeiro projeto/i},{members:1, _id:0})
var idsUsuariosPrimeiroProjeto = []
usuariosPrimeiroProjeto.members.forEach(function (user) {
  idsUsuariosPrimeiroProjeto.push(user.id_user)
})

db.users.find({_id: {$not: {$in: idsUsuariosPrimeiroProjeto}}}, {name: 1})
{
  "_id": ObjectId("56807d83e15bcf96ff94afc5"),
  "name": "Adriana Castelhano"
}
{
  "_id": ObjectId("56807d83e15bcf96ff94afcb"),
  "name": "Nádia Santos"
}
{
  "_id": ObjectId("56807d83e15bcf96ff94afcc"),
  "name": "Palo Tamoio"
}
{
  "_id": ObjectId("56807d83e15bcf96ff94afcd"),
  "name": "Silvana Jordão"
}
{
  "_id": ObjectId("56807d83e15bcf96ff94afce"),
  "name": "Virgínia Remígio"
}
```

## Update - alteração

#### 1. Adicione para todos os projetos o campo views: 0.

```
var query = {}
var mod = {$set: {views: 0}}
var options = {multi: true}
db.projects.update(query, mod, options)

Updated 5 existing record(s) in 118ms
WriteResult({
  "nMatched": 5,
  "nUpserted": 0,
  "nModified": 5
})  
```

#### 2. Adicione 1 tag diferente para cada projeto.

```
```

#### 3. Adicione 2 membros diferentes para cada projeto.

```
```

#### 4. Adicione 1 comentário em cada atividade, deixe apenas 1 projeto sem.

```
```

#### 5. Adicione 1 projeto inteiro com UPSERT.

```
```

## Delete - remoção

## Sharding
// coloque aqui todos os comandos que você executou

## Replica
// coloque aqui todos os comandos que você executou
