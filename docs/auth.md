## Généralité
L'access token est valide Durans 24h passez se delais il faudras faudras reinteroger la route [POST v1/oauth]()


## POST v1/oauth
Route qui permet de recuperer le token qui va vous permetre d'intragire avec l'api 

```
{
    "token":string,
    "secret":string
}
```

### Reponce 

Lors d'un Success

```
POST v1/oauth 200
body: 
{
  "access_token": string
}
```

Si le token ou le secret son erroné

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

Si le token n'ai pas dans le body

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

Si le secret n'ai pas dans le body

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