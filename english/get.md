## Get

### Route
[GET /v1/weproov](#get-v1weproov)  
[GET /v1/weproov/pending]()  
[GET /v1/weproov/dropoff]()  
[GET /v1/weproov/finished]()  

### General Information

All roads take a *lang* setting that allows to translate the title/description field.

A *custom_ref* field allows you to examine with your own *id*.

### GET /v1/weproov

This setting allows you to recover your whole completed WeProov history. 

#### Applicable settings

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

Search request exemple with a **ProovCode** :

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

Search request exemple with **CustomRef** and asking for french as return language :

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

### Error Case

If you search with a **ProovCode** and it is nowhere to be found : 

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

If you search with a **customRef** and it is nowhere to be found : 

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
