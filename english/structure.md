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

### General informations

All keys are written in *snake case*, words are seperated by a _ 

All **title/description** can be translated with a setting **lang** in the URL. 

If a value is not filled, it will not be in the structure.

All structures include a sub-structure position.

If a value is not filled when return, the field is preceded by dropoff_ :

```
value -> dropoff_value // pour les champs infos/checklist
url -> dropoff_url // pour les champs support/process
```


## Type Position

The type position allows you to navigate easily in the structure :
```
{
	"parts": int,
	"infos": string // exemple: "name" ...
}
```

## Type Info

The info filds define the first visible section in the app :

#### Definition:

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
  "infos": [Annotation]
  "dropoff_url": string,
  "dropoff_infos": [Annotation]
  "position": struct_position
}
```

## Type Annotation
```
{
  "index": Int,
  "choice": String, // "Scratch" | "Denting / Embossing" | "Breaking" | "Shard / Breakage" | "Missing piece" | "Another"
  "description": String
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

## type Geo-tag 

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
