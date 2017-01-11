## Initiate a WeProov

[GET /v1/weproov/template]()  
[GET /v1/weproov/init/:template_id]()
[POST /v1/weproov/init/:template_id]()

## GET /v1/weproov/template

Allows to recover the ful template list

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

Allows to create a new report from an existing template.

If you want to **initiate** and **update** the informations you can use a **POST** request with a body that must be the same as the one while an update.

### Applicable settings

```
lang: permet de choisir la lang de retour du WeProov
```

### Return

Upon a success, a code 200 and a WeProov structure will be sent back.  

### Exemple
If everything succeeded with a custom_ref : 

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

If the template is nowhere to be found : 

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

