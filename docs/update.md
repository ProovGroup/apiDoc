[POST /v1/weproov](#post-v1weproov)

## update

### Généralités

Pour cette route, les champs pouvant être mis à jour sont toutes les infos, sauf les types **list**.


### Structure pour le push des informations

la structure est composée de deux élèments :  la **position**, qui permet de seléctionner un champ à *update* et la **valeur** à *set*.

```
{
	value: string | boolean | int, 
	position: struct_position // Obligatoire
}
```

### Pour trouvez la position il existe deux solutions

#### Via l'API

Lors de la récupération d'un WeProov via la requête [GET /v1/weproov]() avec un paramètre **proov_code** ou **custom_ref** les positions sont visibles.

### Via L'application

Pour vous l'expliquer nous allons utiliser un template défini comme ceci:

- Propriétaire 
	- infos:
		- nom
		- prénom 
		- e-mail
		- numéro de téléphone
	
- locataire 
	- infos:
		- nom
		- prénom 
		- e-mail
		- numéro de téléphone

	- checklists:
		- carte d'identité à présenter
		- a plus de 18 ans

- Véhicule
	- infos
		- Immatriculation
		- Kilométrage
	
	- checklists
		- Nombre de gilets
		- Roue de secours
		

lorsque vous ouvrez ce Template, vous arrivez sur un premier onglet, celui-ci correspond aux infos du propriétaire **position: {parts: 0}**.

la Première info, le *nom*, correspond à  **position: {parts: 0, infos: 0}**.
la second info le *prenom* correspond a  **position: {parts: 0, infos: 1}** ainsi de suite.

donc si nous reprenons notre template nous obtenons ceci:

- Propriétaire -> **position: {parts: 0}**
	- infos:
		- nom -> **position: {parts: 0, infos: 0}**
		- prénom -> **position: {parts: 0, infos: 1}**
		- e-mail -> **position: {parts: 0, infos: 2}**
		- numéro de téléphone -> **position: {parts: 0, infos: 3}**

Changeons d'onglet. vous arrivez sur la partie locataire, celle-ci étant la deuxième partie, elle correspond à **position: {parts: 1}**.
Le schéma sera le même mais cette partie a une *checklists*. Pour atteindre une *checklists* il suffit de remplacer la clé *infos* par *checklists* et repartir de 0.

Donc si nous reprenons notre template nous obtenons ceci:

- locataire -> **position: {parts: 1}**
	- infos:
		- nom -> **position: {parts: 1, infos: 0}**
		- prénom -> **position: {parts: 1, infos: 1}**
		- e-mail -> **position: {parts: 1, infos: 2}**
		- numéro de téléphone -> **position: {parts: 1, infos: 3}**

	- checklists:
		- carte d'identité  présentée **position: {parts: 1, checklists: 0}**
		- à plus de 18 ans -> **position: {parts: 1, checklists: 0}**

pour finir il reste la partie Véhicule donc changeons encore une fois d'onglet. Nous pouvons distinguer le bien par son logo dans la barre de navigation. Cet onglet correspond à **position: {items: 0}**.

de la même facon nous pouvons nous balader dans les différents champs, ce qui nous donne: 

- Vehicule -> **position: {items: 0}**
	- infos
		- Immatriculation -> **position: {items: 0, infos: 0}**
		- Kilométrage -> **position: {items: 0, infos: 1}**
	
	- checklists
		- Nombre de gilets -> **position: {items: 0, checklists: 0}**
		- Roue de secours -> **position: {items: 0, checklists: 1}**

### POST /v1/weproov

Route pour push des informations dans un WeProov :

Le body dois être composé d'un **Array** contenant de structure définie plus bas.

Exemple:

```
[
	{
		value: "Craig", 
		position: {parts: 0, infos: 0}
	},
	{
		value: "Daniel", 
		position: {parts: 0, infos: 1}
	},
	{
		value: "0606060606", 
		position: {parts: 0, infos: 2}
	},
	{
		value: "daniel.craig@yopmail.com", 
		position: {parts: 0, infos: 3}
	},
	{
		value: "AA-BBB-CCC", 
		position: {items: 0, infos: 0}
	},
	{
		value: "552345", 
		position: {items: 0, infos: 1}
	},
	{
		value: 3, 
		position: {items: 0, checklists: 0}
	},
	{
		value: true, 
		position: {items: 0, checklists: 1}
	}
]
```

### Cas d'erreur

Si un WeProov n'est pas trouvé :

```
{
  "status": 404,
  "errors": [
    {
      "code": 404,
      "type": "WEPROOV_NOT_FOUND",
      "message": "Error WeProov not found",
      "timestamp": 1457532001
    }
  ],
  "timestamp": 1457532001
}
```

Si un WeProov n'est pas éditable :

```
{
  "status": 401,
  "errors": [
    {
      "code": 401,
      "type": "WEPROOV_NOT_EDITABLE",
      "message": "Error WeProov is not editable",
      "timestamp": 1457532001
    }
  ],
  "timestamp": 1457532001
}
```


Si une structure ne contient pas la position de l'*infos* ou du *checklists* :  

```
{
  "status": 400,
  "errors": [
    {
      "code": 400,
      "type": "INCORECT_POSITION",
      "message": "Position need infos or checklists information",
      "timestamp": 1457532001
    }
  ],
  "timestamp": 1457532001
}
```

Si une structure ne contient pas la position de la *parts* ou de l'*items* 

```
{
  "status": 400,
  "errors": [
    {
      "code": 400,
      "type": "INCORECT_POSITION",
      "message": "Position need parts or items informations",
      "timestamp": 1457532001
    }
  ],
  "timestamp": 1457532001
}
```

Si aucune structure *position* n'a été trouvée

```
{
  "status": 400,
  "errors": [
    {
      "code": 400,
      "type": "NOT_POSITION",
      "message": "Update Object don't have position",
      "timestamp": 1457532001
    }
  ],
  "timestamp": 1457532001
}
```