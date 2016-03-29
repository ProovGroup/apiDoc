## Structure

[Position](#type-position)  
[Info](#type-info)  
[Checklist](#type-checklist)  
[Support](#type-support)  
[Part](#type-part)  
[Process](#type-process)  
[Item](#type-item)  
[Géoloc](#type-géoloc)  
[WeProov](#type-weproov)  

### Généralités

Toutes les clés sont écrites en *snake case*, les mots sont separés par un _ 

Tous les **title/description** peuvent être traduits par un paramètre **lang** dans l'url. 

Si une valeur n'est pas renseignée, elle ne sera pas présente dans la structure.

Toutes les structures comportent une sous-structure position.

Si une valeur a été définie lors d'un retour, le champs sera préfixé par dropoff_ :

```
value -> dropoff_value // pour les champs infos/checklist
url -> dropoff_url // pour les champs support/process
```


## Type Position

Le type position permet de naviguer facilement dans la structure :
```
{
	"parts": int,
	"infos": int
}
```

## Type Info

Les champs infos définissent la première section visible dans l'application :

#### Définition:

```
{
  "name": string,
  "title": string,
  "value": string,
  "dropoff_value": string,
  "position": struct_position
}
```

## type Checklist

```
{
  "name": string,
  "title": string,
  "value": boolean ou int,
  "dropoff_value": boolean ou int,
  "position": struct_position
}
```

## type Support

```
{
  "name": string,
  "title": string,
  "url": string,
  "dropoff_url": string,
  "position": struct_position
}
```

## type Part

```
{
	"title": string,
	"infos": [struct_info],
	"supports": [struct_support],
	"checklists": [struct_checklist],
	"position": struct_position
}
```

## type Process
```
{
  "name": string,
  "title": string,
  "url": string,
  "dropoff_url": string,
  "position": struct_position
}
```

## type Item
```
{
	"title": string,
	"infos": [struct_info],
	"supports": [struct_support],
	"checklists": [struct_checklist],
	"process": [struct_process],
	"position": struct_position
}
```

## type Géoloc 

```
{
	"full_address": string,
	"longitude": float,
	"latitude": float
}
```

## Type WeProov 

```
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
