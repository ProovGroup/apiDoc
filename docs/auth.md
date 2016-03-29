## Généralité
L'**access_token** n'est valide que 24h. Passé ce délai, il faudra réinterroger la route [POST v1/oauth]().

L'**access_token** doit être placé dans le header, dans le champ Authorization 
exemple:
```
'Authorization: Bearer <auth_token>' 
```

## POST v1/oauth
[POST v1/oauth]() et l'objet suivant, permettent de récupérer le token permettant d'intéragir avec l'api  :

```
{
    "token":string,
    "secret":string
}
```

### Réponse 

Lors d'un *Success* :

```
POST v1/oauth 200
body: 
{
  "access_token": string
}
```

Si le **token** ou le **secret** est erroné :

```
POST v1/oauth 401
body:
{
  "status": 401,
  "errors": [
    {
      "code": 401,
      "type": "BAD_TOKEN_OR_SECRET",
      "timestamp": 1458226719
    }
  ],
  "timestamp": 1458226719
}
```

Si le **token** n'est pas dans le **body** :

```
POST v1/oauth 400
{
  "status": 400,
  "errors": [
    {
      "code": 400,
      "type": "TOKEN_NOT_FOUND",
      "timestamp": 1458226765
    }
  ],
  "timestamp": 1458226765
}
```

Si le **secret** n'est pas dans le **body** :

```
POST v1/oauth 400
{
  "status": 400,
  "errors": [
    {
      "code": 400,
      "type": "SECRET_NOT_FOUND",
      "timestamp": 1458226811
    }
  ],
  "timestamp": 1458226811
}
```
