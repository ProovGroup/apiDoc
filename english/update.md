[PUT /v1/weproov](#put-v1weproov)

## update

### General informations

For this road, the fields that can be updated are the info filds, except the **list** types.


### Information push structure

Two elements compose the structure : **position**, that allows you to select a field to *update* and the **valeur** to *set*.

```
{
	value: string | boolean | int, 
	position: struct_position // Obligatoire
}
```

### To find the position, there are two solutions

#### Through the API

When you recover a WeProov with the [GET /v1/weproov]() request with a **proov_code** setting or **custom_ref** the positions are visible.

### Through the Application

To explain, we will use a template built as followed:

- Owner 
	- infos:
		- name
		- first name 
		- e-mail
		- phone number
	
- Tenant 
	- infos:
		- name
		- first name 
		- e-mail
		- phone number

	- checklists:
		- ID checked
		- is 21 or above

- Véhicule
	- infos
		- Vehicle ID
		- Mileage
	
	- checklists
		- Emergency jacket number
		- Spare wheel
		

When you open this Template, vyou get to the first tab, the owner infos **position: {parts: 0}**.

The first one, *nom*, is  **position: {parts: 0, infos: "name"}**.
Teh second one, *prenom*, is  **position: {parts: 0, infos: "first_name"}**, and so on.

So, if we take back our template, we get this :

- Owner -> **position: {parts: 0}**
	- infos:
		- name -> **position: {parts: 0, infos: "name"}**
		- first name -> **position: {parts: 0, infos: "first_name"}**
		- e-mail -> **position: {parts: 0, infos: "email"}**
		- phone number -> **position: {parts: 0, infos: "phone_number"}**

Let's change the tab. You are on the tenant tab, the second stakeholder in a way, it is **position: {parts: 1}**.
The pattern is the same but this part has a *checklists*. To reach a checklist *checklists* you only have to replace the key *infos* by *checklists*.

So, if we take back our template, we get this :

- Tenant -> **position: {parts: 0}**
	- infos:
		- name -> **position: {parts: 0, infos: "name"}**
		- first name -> **position: {parts: 0, infos: "first_name"}**
		- e-mail -> **position: {parts: 0, infos: "email"}**
		- phone number -> **position: {parts: 0, infos: "phone_number"}**

	- checklists:
		- ID checked **position: {parts: 1, checklists: "valid_id"}**
		- Is 21 and above -> **position: {parts: 1, checklists: "older_than_18"}**

Finally, you have the vehicle part, so let's change the tab again. This tab is **position: {items: 0}**.

Like earlier, we can navigate through the different fields, and that gives us : 

- Vehicule -> **position: {items: 0}**
	- infos
		- Vehicle ID -> **position: {items: 0, infos: "register"}**
		- Mileage -> **position: {items: 0, infos: "kilometers"}**
	
	- checklists
		- Emergency jacket number -> **position: {items: 0, checklists: "security_vest"}**
		- Spare wheel -> **position: {items: 0, checklists: "spare_wheel"}**

### put /v1/weproov

Road to push the info in a WeProov :

The body must be composed with an **Array** containing the structures defined lower.

Exemple:

```
[
	{
		value: "Craig", 
		position: {parts: 0, infos: "name"}
	},
	{
		value: "Daniel", 
		position: {parts: 0, infos: "first_name"}
	},
	{
		value: "0606060606", 
		position: {parts: 0, infos: "phone_number"}
	},
	{
		value: "daniel.craig@yopmail.com", 
		position: {parts: 0, infos: "email"}
	},
	{
		value: "AA-BBB-CCC", 
		position: {items: 0, infos: "register"}
	},
	{
		value: "552345", 
		position: {items: 0, infos: "kilometers"}
	},
	{
		value: 3, 
		position: {items: 0, checklists: "security_vest"}
	},
	{
		value: true, 
		position: {items: 0, checklists: "spare_wheel"}
	}
]
```

### Error case

If the WeProov is nowhere to be found :

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

If the WeProov can not be edited :

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


If the structure does not contain the position of the *infos* or the *checklists* :  

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

If the structure does not contain the position of the *parts* or the *items* 

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

If no structure *position* can be found

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
