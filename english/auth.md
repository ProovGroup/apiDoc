## Information
The **access_token** is only available for 24h. When you passed this deadline, you need to re-examine the road [POST v1/oauth]().

The **access_token** must be placed in the header, in the Authorization field. 
Exemple :
```
'Authorization: Bearer <auth_token>' 
```

## POST v1/oauth
[POST v1/oauth]() and the next object allow you to recover the token that leads you to interact with the api :

```
{
    "token":string,
    "secret":string
}
```

### Response 

When *Success* :

```
POST v1/oauth 200
body: 
{
  "access_token": string
}
```

If the **token** or the **secret** is wrong :

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

If the **token** is not in the **body** :

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

If the **secret** is not in the **body** :

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
