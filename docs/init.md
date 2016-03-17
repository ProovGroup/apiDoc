## Initier un WeProov

[GET /v1/weproov/template]()  
[GET /v1/weproov/init/:template_id]()

## GET /v1/weproov/template

permet de récupérer la liste de tout les templates

### Paramètre applicable

```
lang: permet de choisir la langue de retour
```

### Exemple

```
GET /v1/weproov/template 200

body:
[
  {
    "id": int, // id à utiliser pour l'initialisation
    "title": string,
    "description": string,
    "dropoff": boolean, // permets de savoir si le WeProov passeras par le state 'dropoff'
    "full_dropoff": boolean // permets de savoir si au retour toutes les photos process seront reprises
  }
]
```

## GET /v1/weproov/:template_id

Permet de créer un nouveaux rapport à partir d'un template préalablement établi.

Si vous désirez **initialiser** et **update** les informations vous pouvez utiliser une requête **POST** avec un body qui doit être le même que lors d'un update.

### Paramètre applicable

```
lang: permet de choisir la lang de retour du WeProov
```

### Retour

lor d'un success un code 200 sera retourné ainsi qu'une structure WeProov.  

### Exemple
Si tout s'est bien passé en mettant un custom_ref : 

```
GET /v1/weproov/init/1?lang=fr&custom_ref=AA-AA-AA 200

body:
{
	"title": string,
	"description": string,
	"parts": [struct_part],
	"items": [struct_item],
	"finished_at": isoTime,
	"proov_code": string,
	"custom_ref": string,
	"state": string,
	"template": int,
	"pdf": string,
	"geoloc": stuct_geoloc,
	"dropoff_geoloc": struc_geoloc,
	"pdf": string,
	"dropoff_pdf": string,
}
```

Si le Template n'est pas trouvé : 

```
GET /v1/weproov/init/199 404

body:
{
  "status": 404,
  "errors": [
    {
      "code": 404,
      "type": "TEMPLATE_NOT_FOUND",
      "message": "No template found with id 199",
      "timestamp": 1457452056
    }
  ],
  "timestamp": 1457452056
}
```

