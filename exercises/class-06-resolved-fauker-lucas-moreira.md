# Mongo DB - Aula 06 - Parte 02 - Exercício 

Autor: **Lucas Moreira**


## Criar um índice para o campo name e um índice conjunto para qualquer outros campos

```
db.pokemons.createIndex({ name: 1 })
db.system.indexes.find()
{
  "v": 1,
  "key": {
    "_id": 1
  },
  "name": "_id_",
  "ns": "be-mean.teste"
}
{
  "v": 1,
  "key": {
    "_id": 1
  },
  "name": "_id_",
  "ns": "be-mean.pokemons"
}
{
  "v": 1,
  "key": {
    "_id": 1
  },
  "name": "_id_",
  "ns": "be-mean.restaurantes"
}
{
  "v": 1,
  "key": {
    "name": 1
  },
  "name": "name_1",
  "ns": "be-mean.pokemons"
}

```

##3. Rodar uma query sem índice para o campo nome e uma com índice para o campo nome

```
**Sem índice**:

db.pokemons.find({ name: 'Charmander' }).explain("executionStats")
{
  "queryPlanner": {
    "plannerVersion": 1,
    "namespace": "be-mean.pokemons",
    "indexFilterSet": false,
    "parsedQuery": {
      "name": {
        "$eq": "Charmander"
      }
    },
    "winningPlan": {
      "stage": "COLLSCAN",
      "filter": {
        "name": {
          "$eq": "Charmander"
        }
      },
      "direction": "forward"
    },
    "rejectedPlans": [ ]
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 1,
    "executionTimeMillis": 5,
    "totalKeysExamined": 0,
    "totalDocsExamined": 610,
    "executionStages": {
      "stage": "COLLSCAN",
      "filter": {
        "name": {
          "$eq": "Charmander"
        }
      },
      "nReturned": 1,
      "executionTimeMillisEstimate": 10,
      "works": 612,
      "advanced": 1,
      "needTime": 610,
      "needFetch": 0,
      "saveState": 4,
      "restoreState": 4,
      "isEOF": 1,
      "invalidates": 0,
      "direction": "forward",
      "docsExamined": 610
    }
  },
  "serverInfo": {
    "host": "MacBook-Pro-de-Lucas.local",
    "port": 27017,
    "version": "3.0.7",
    "gitVersion": "nogitversion"
  },
  "ok": 1
}

**Com índice:

db.pokemons.createIndex({ name: 1})

db.pokemons.find({ name: 'Charmander' }).explain("executionStats")
{
  "queryPlanner": {
    "plannerVersion": 1,
    "namespace": "be-mean.pokemons",
    "indexFilterSet": false,
    "parsedQuery": {
      "name": {
        "$eq": "Charmander"
      }
    },
    "winningPlan": {
      "stage": "FETCH",
      "inputStage": {
        "stage": "IXSCAN",
        "keyPattern": {
          "name": 1
        },
        "indexName": "name_1",
        "isMultiKey": false,
        "direction": "forward",
        "indexBounds": {
          "name": [
            "[\"Charmander\", \"Charmander\"]"
          ]
        }
      }
    },
    "rejectedPlans": [ ]
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 1,
    "executionTimeMillis": 0,
    "totalKeysExamined": 1,
    "totalDocsExamined": 1,
    "executionStages": {
      "stage": "FETCH",
      "nReturned": 1,
      "executionTimeMillisEstimate": 0,
      "works": 2,
      "advanced": 1,
      "needTime": 0,
      "needFetch": 0,
      "saveState": 0,
      "restoreState": 0,
      "isEOF": 1,
      "invalidates": 0,
      "docsExamined": 1,
      "alreadyHasObj": 0,
      "inputStage": {
        "stage": "IXSCAN",
        "nReturned": 1,
        "executionTimeMillisEstimate": 0,
        "works": 2,
        "advanced": 1,
        "needTime": 0,
        "needFetch": 0,
        "saveState": 0,
        "restoreState": 0,
        "isEOF": 1,
        "invalidates": 0,
        "keyPattern": {
          "name": 1
        },
        "indexName": "name_1",
        "isMultiKey": false,
        "direction": "forward",
        "indexBounds": {
          "name": [
            "[\"Charmander\", \"Charmander\"]"
          ]
        },
        "keysExamined": 1,
        "dupsTested": 0,
        "dupsDropped": 0,
        "seenInvalidated": 0,
        "matchTested": 0
      }
    }
  },
  "serverInfo": {
    "host": "MacBook-Pro-de-Lucas.local",
    "port": 27017,
    "version": "3.0.7",
    "gitVersion": "nogitversion"
  },
  "ok": 1
}
```

##4. Rodar uma query sem índice para os campos conjuntos e uma query com índice para os campos conjuntos

```
**Sem índice**:

db.pokemons.find({ $and: [{name: 'Charmander'}, {defense: 43}] }).explain("executionStats")
{
  "queryPlanner": {
    "plannerVersion": 1,
    "namespace": "be-mean.pokemons",
    "indexFilterSet": false,
    "parsedQuery": {
      "$and": [
        {
          "defense": {
            "$eq": 43
          }
        },
        {
          "name": {
            "$eq": "Charmander"
          }
        }
      ]
    },
    "winningPlan": {
      "stage": "COLLSCAN",
      "filter": {
        "$and": [
          {
            "defense": {
              "$eq": 43
            }
          },
          {
            "name": {
              "$eq": "Charmander"
            }
          }
        ]
      },
      "direction": "forward"
    },
    "rejectedPlans": [ ]
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 1,
    "executionTimeMillis": 3,
    "totalKeysExamined": 0,
    "totalDocsExamined": 610,
    "executionStages": {
      "stage": "COLLSCAN",
      "filter": {
        "$and": [
          {
            "defense": {
              "$eq": 43
            }
          },
          {
            "name": {
              "$eq": "Charmander"
            }
          }
        ]
      },
      "nReturned": 1,
      "executionTimeMillisEstimate": 0,
      "works": 612,
      "advanced": 1,
      "needTime": 610,
      "needFetch": 0,
      "saveState": 4,
      "restoreState": 4,
      "isEOF": 1,
      "invalidates": 0,
      "direction": "forward",
      "docsExamined": 610
    }
  },
  "serverInfo": {
    "host": "MacBook-Pro-de-Lucas.local",
    "port": 27017,
    "version": "3.0.7",
    "gitVersion": "nogitversion"
  },
  "ok": 1
}

**Com índice**:

db.pokemons.createIndex({ name: 1, defense: 1 })

db.pokemons.find({ $and: [{name: 'Charmander'}, {defense: 43}] }).explain("executionStats")
{
  "queryPlanner": {
    "plannerVersion": 1,
    "namespace": "be-mean.pokemons",
    "indexFilterSet": false,
    "parsedQuery": {
      "$and": [
        {
          "defense": {
            "$eq": 43
          }
        },
        {
          "name": {
            "$eq": "Charmander"
          }
        }
      ]
    },
    "winningPlan": {
      "stage": "FETCH",
      "inputStage": {
        "stage": "IXSCAN",
        "keyPattern": {
          "name": 1,
          "defense": 1
        },
        "indexName": "name_1_defense_1",
        "isMultiKey": false,
        "direction": "forward",
        "indexBounds": {
          "name": [
            "[\"Charmander\", \"Charmander\"]"
          ],
          "defense": [
            "[43.0, 43.0]"
          ]
        }
      }
    },
    "rejectedPlans": [ ]
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 1,
    "executionTimeMillis": 0,
    "totalKeysExamined": 1,
    "totalDocsExamined": 1,
    "executionStages": {
      "stage": "FETCH",
      "nReturned": 1,
      "executionTimeMillisEstimate": 0,
      "works": 2,
      "advanced": 1,
      "needTime": 0,
      "needFetch": 0,
      "saveState": 0,
      "restoreState": 0,
      "isEOF": 1,
      "invalidates": 0,
      "docsExamined": 1,
      "alreadyHasObj": 0,
      "inputStage": {
        "stage": "IXSCAN",
        "nReturned": 1,
        "executionTimeMillisEstimate": 0,
        "works": 2,
        "advanced": 1,
        "needTime": 0,
        "needFetch": 0,
        "saveState": 0,
        "restoreState": 0,
        "isEOF": 1,
        "invalidates": 0,
        "keyPattern": {
          "name": 1,
          "defense": 1
        },
        "indexName": "name_1_defense_1",
        "isMultiKey": false,
        "direction": "forward",
        "indexBounds": {
          "name": [
            "[\"Charmander\", \"Charmander\"]"
          ],
          "defense": [
            "[43.0, 43.0]"
          ]
        },
        "keysExamined": 1,
        "dupsTested": 0,
        "dupsDropped": 0,
        "seenInvalidated": 0,
        "matchTested": 0
      }
    }
  },
  "serverInfo": {
    "host": "MacBook-Pro-de-Lucas.local",
    "port": 27017,
    "version": "3.0.7",
    "gitVersion": "nogitversion"
  },
  "ok": 1
}
```
