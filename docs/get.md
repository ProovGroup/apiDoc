## Get

### Route
[GET /v1/weproov](#get-v1weproov)  
[GET /v1/weproov/pending]()  
[GET /v1/weproov/dropoff]() 
[GET /v1/weproov/history]()  

### Généralités

Toutes les routes prennent un paramètre *lang* qui permet de traduire les champs title/description.

Un champs *custom_ref* permet d'interroger avec votre propre *id*.

### GET /v1/weproov

Ce paramètre vous permet de récupérer tout l'historique de vos WeProov effectués. 

#### Paramètre applicable

```
lang: permet de choisir la langue de retour 
proovcode: permet de récuperer un weproov par son proovcode
custom_ref: permet de recuperer un weproov par une custom référence set auparavant
```

#### Exemple

```
GET /v1/weproov 200

body:
[
	{
		"title": string,
		"description": string,
		"finished_at": isoTime,
		"proov_code": string,
		"state": string,
		"template": int,
		"pdf": string,
		"geoloc": stuct_geoloc,
		"dropoff_geoloc": struc_geoloc,
		"pdf": string,
		"dropoff_pdf": string,
	},
	{
		"title": string,
		"description": string,
		"finished_at": isoTime,
		"proov_code": string,
		"state": string,
		"template": int,
		"pdf": string,
		"geoloc": stuct_geoloc,
		"dropoff_geoloc": struc_geoloc,
		"pdf": string,
		"dropoff_pdf": string,
	}, ...
]
```

Exemple de requête de recherche par **ProovCode** :

```
GET /v1/weproov?proov_code=AAAAAA 200

body:
{
	"title": string,
	"description": string,
	"parts": [struct_part],
	"items": [struct_item],
	"finished_at": isoTime,
	"proov_code": string,
	"state": string,
	"template": int,
	"pdf": string,
	"geoloc": stuct_geoloc,
	"dropoff_geoloc": struc_geoloc,
	"pdf": string,
	"dropoff_pdf": string,
}
```

Exemple de requête de recherche par **CustomRef** et demandant la langue française comme retour :

```
GET /v1/weproov?custom_ref=MyCustomRef 200

body:
{
	"title": string,
	"description": string,
	"parts": [struct_part],
	"items": [struct_item],
	"finished_at": isoTime,
	"proov_code": string,
	"state": string,
	"template": int,
	"pdf": string,
	"geoloc": stuct_geoloc,
	"dropoff_geoloc": struc_geoloc,
	"pdf": string,
	"dropoff_pdf": string,
}
```

### Cas d'erreur

Si vous recherchez par **ProovCode** et qu'il n'est pas trouvé : 

```
GET /v1/weproov?proov_code=FAUX_PROOVCODE 404

body:
{
  "status": 404,
  "errors": [
    {
      "code": 404,
      "type": "PROOV_CODE_NOT_FOUND",
      "message": "ProovCode not found",
      "timestamp": 1457450378
    }
  ],
  "timestamp": 1457450378
}
```

Si vous recherchez par **customRef** et qu'elle n'est pas trouvée : 

```
GET /v1/weproov?custom_ref=FAUSSE_REFERENCE 404

body:
{
  "status": 404,
  "errors": [
    {
      "code": 404,
      "type": "CUSTOM_REF_NOT_FOUND",
      "message": "Custom ref not found",
      "timestamp": 1457450378
    }
  ],
  "timestamp": 1457450378
}
```
