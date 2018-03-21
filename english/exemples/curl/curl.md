## Authentification

# Request 
```
curl -H "Content-Type: application/json" \
	-d '{ 
		"token": "<TOKEN>", 
		"secret": "<SECRET>" 
	}' \
	-X POST \
	https://api.weproov.com/v1/oauth
```

# Réponse

```
{
  "access_token": "<ACCESS_TOKEN>"
}
```

## GET TEMPLATE

# Request 
```
curl -H "Content-Type: application/json" \
	-H "Authorization: Bearer <ACCESS_TOKEN>" \
	-X GET \
	https://api.weproov.com/v1/weproov/template
```

# Réponse 

```
[
  {
    "id": TEMPLATE_ID,
    "title": TITLE OF TEMPLATE,
    "description": DESCRIPTION OF TEMPLATE,
    "dropoff": true,
    "full_dropoff": false
  }
]
```

## INIT TEMPLATE (sans donnée)

# Request 
```
curl -H "Content-Type: application/json" \
	-H "Authorization: Bearer <ACCESS_TOKEN>" \
	-X GET \
	https://api.weproov.com/v1/weproov/init/:template_id
```

# Réponse 
voire la partie structure pour avoir plus d'information
```
{
  "title": "CERTIFIED CONDITION REPORT",
  "description": "Je réalise l'état des lieux au moment de ma prise de poste.",
  "proov_code": "XPYWJ7",
  "state": "pending_first",
  "template": 218,
  "parts": [
    {
      "title": "Tenant",
      "infos": [
        {
          "name": "company_name",
          "title": "Company Name",
          "value": "ProovGroup",
          "position": {
            "parts": 0,
            "infos": 0
          }
        }
      ],
      "supports": [],
      "checklists": [],
      "position": {
        "parts": 0
      }
    },
    {
      "title": "Customer",
      "infos": [
        {
          "name": "email",
          "title": "Email",
          "position": {
            "parts": 1,
            "infos": 0
          }
        },
        {
          "name": "name",
          "title": "Name",
          "position": {
            "parts": 1,
            "infos": 1
          }
        },
        {
          "name": "first_name",
          "title": "First name",
          "position": {
            "parts": 1,
            "infos": 2
          }
        },
        {
          "name": "phone_number",
          "title": "Cell Phone",
          "position": {
            "parts": 1,
            "infos": 3
          }
        }
      ],
      "supports": [],
      "checklists": [],
      "position": {
        "parts": 1
      }
    }
  ],
  "items": [
    {
      "title": "Item",
      "infos": [
        {
          "name": "register",
          "title": "Vehicle Licence Plate",
          "position": {
            "items": 0,
            "infos": 0
          }
        },
        {
          "name": "wp_weather_condition",
          "title": "WeProov condition",
          "position": {
            "items": 0,
            "infos": 1
          }
        },
        {
          "name": "interior_condition",
          "title": "State of exterior cleanliness",
          "position": {
            "items": 0,
            "infos": 2
          }
        },
        {
          "name": "vehicle_color",
          "title": "Colour",
          "position": {
            "items": 0,
            "infos": 3
          }
        }
      ],
      "supports": [
        {
          "name": "rental_contract",
          "title": "Rental Contract",
          "position": {
            "items": 0,
            "supports": 0
          }
        },
        {
          "name": "condition_report_paper",
          "title": "Paper Vehicle Condition Report",
          "position": {
            "items": 0,
            "supports": 1
          }
        },
        {
          "name": "written_proof_picture",
          "title": "Written Proof picture",
          "position": {
            "items": 0,
            "supports": 2
          }
        },
        {
          "name": "other_document",
          "title": "Other document",
          "position": {
            "items": 0,
            "supports": 3
          }
        }
      ],
      "checklists": [
        {
          "name": "ac_tested",
          "title": "A/C Tested",
          "value": false,
          "dropoff_value": false,
          "position": {
            "items": 0,
            "checklists": 0
          }
        },
        {
          "name": "keys_tested",
          "title": "Key(s) tested ?",
          "value": false,
          "dropoff_value": false,
          "position": {
            "items": 0,
            "checklists": 1
          }
        },
        {
          "name": "number_keys",
          "title": "Number of given keys",
          "position": {
            "items": 0,
            "checklists": 2
          }
        }
      ],
      "position": {
        "items": 0
      },
      "process": []
    }
  ]
}
```

## INIT TEMPLATE (avec donnée)

La commande suivant permet de rentrer le nom/prénom, de la partie  numéro 1 ainsi que la plaque d'immatriculation du véhicule.
# Request 
```
curl -H "Content-Type: application/json" \
	-H "Authorization: Bearer <ACCESS_TOKEN>" \
	-d '[
		{
			"value": "Craig", 
			"position": {"parts": 1, "infos": "name"}
		},
		{
			"value": "Daniel", 
			"position": {"parts": 1, "infos": "first_name"}
		},
		{
			"value": "AA-BB-CCC", 
			"position": {"items": 0, "infos": "register"}
		}
	]' \
	-X POST \
	https://api.weproov.com/v1/weproov/init/:template_id
```

# Réponse 

```
{
  "title": "CERTIFIED CONDITION REPORT",
  "description": "Je réalise l'état des lieux au moment de ma prise de poste.",
  "proov_code": "8RWQ33",
  "state": "pending",
  "template": 218,
  "parts": [
    {
      "title": "Tenant",
      "infos": [
        {
          "name": "company_name",
          "title": "Company Name",
          "value": "ProovGroup",
          "position": {
            "parts": 0,
            "infos": 0
          }
        }
      ],
      "supports": [],
      "checklists": [],
      "position": {
        "parts": 0
      }
    },
    {
      "title": "Customer",
      "infos": [
        {
          "name": "email",
          "title": "Email",
          "position": {
            "parts": 1,
            "infos": 0
          }
        },
        {
          "name": "name",
          "title": "Name",
          "value": "Craig",
          "position": {
            "parts": 1,
            "infos": 1
          }
        },
        {
          "name": "first_name",
          "title": "First name",
          "value": "Daniel",
          "position": {
            "parts": 1,
            "infos": 2
          }
        },
        {
          "name": "phone_number",
          "title": "Cell Phone",
          "position": {
            "parts": 1,
            "infos": 3
          }
        }
      ],
      "supports": [],
      "checklists": [],
      "position": {
        "parts": 1
      }
    }
  ],
  "items": [
    {
      "title": "Item",
      "infos": [
        {
          "name": "register",
          "title": "Vehicle Licence Plate",
          "value": "AA-BB-CCC",
          "position": {
            "items": 0,
            "infos": 0
          }
        },
        {
          "name": "wp_weather_condition",
          "title": "WeProov condition",
          "position": {
            "items": 0,
            "infos": 1
          }
        },
        {
          "name": "interior_condition",
          "title": "State of exterior cleanliness",
          "position": {
            "items": 0,
            "infos": 2
          }
        },
        {
          "name": "vehicle_color",
          "title": "Colour",
          "position": {
            "items": 0,
            "infos": 3
          }
        }
      ],
      "supports": [
        {
          "name": "rental_contract",
          "title": "Rental Contract",
          "position": {
            "items": 0,
            "supports": 0
          }
        },
        {
          "name": "condition_report_paper",
          "title": "Paper Vehicle Condition Report",
          "position": {
            "items": 0,
            "supports": 1
          }
        },
        {
          "name": "written_proof_picture",
          "title": "Written Proof picture",
          "position": {
            "items": 0,
            "supports": 2
          }
        },
        {
          "name": "other_document",
          "title": "Other document",
          "position": {
            "items": 0,
            "supports": 3
          }
        }
      ],
      "checklists": [
        {
          "name": "ac_tested",
          "title": "A/C Tested",
          "value": false,
          "dropoff_value": false,
          "position": {
            "items": 0,
            "checklists": 0
          }
        },
        {
          "name": "keys_tested",
          "title": "Key(s) tested ?",
          "value": false,
          "dropoff_value": false,
          "position": {
            "items": 0,
            "checklists": 1
          }
        },
        {
          "name": "number_keys",
          "title": "Number of given keys",
          "position": {
            "items": 0,
            "checklists": 2
          }
        }
      ],
      "position": {
        "items": 0
      },
      "process": []
    }
  ]
}
```

## UPDATE UN WEPROOV (avec donnée)

La commande suivante permet de modifier le ProovCode en changeant le numéro de téléphone (phone_number) de la partie numéro 1.

# Request 
```
curl -H "Content-Type: application/json" \
	-H "Authorization: Bearer <ACCESS_TOKEN>" \
	-d '[
		{
			"value": "0101010101", 
			"position": {"parts": 1, "infos": "phone_number"}
		}
	]' \
	-X PUT \
	https://api.weproov.com/v1/weproov?proov_code="8RWQ33"
```

# Réponse 
```
{
  "title": "CERTIFIED CONDITION REPORT",
  "description": "Je réalise l'état des lieux au moment de ma prise de poste.",
  "proov_code": "8RWQ33",
  "state": "pending",
  "template": 218,
  "parts": [
    {
      "title": "Tenant",
      "infos": [
        {
          "name": "company_name",
          "title": "Company Name",
          "value": "ProovGroup",
          "position": {
            "parts": 0,
            "infos": 0
          }
        }
      ],
      "supports": [],
      "checklists": [],
      "position": {
        "parts": 0
      }
    },
    {
      "title": "Customer",
      "infos": [
        {
          "name": "email",
          "title": "Email",
          "position": {
            "parts": 1,
            "infos": 0
          }
        },
        {
          "name": "name",
          "title": "Name",
          "value": "Craig",
          "position": {
            "parts": 1,
            "infos": 1
          }
        },
        {
          "name": "first_name",
          "title": "First name",
          "value": "Daniel",
          "position": {
            "parts": 1,
            "infos": 2
          }
        },
        {
          "name": "phone_number",
          "title": "Cell Phone",
          "value": "0101010101",
          "position": {
            "parts": 1,
            "infos": 3
          }
        }
      ],
      "supports": [],
      "checklists": [],
      "position": {
        "parts": 1
      }
    }
  ],
  "items": [
    {
      "title": "Item",
      "infos": [
        {
          "name": "register",
          "title": "Vehicle Licence Plate",
          "value": "AA-BB-CCC",
          "position": {
            "items": 0,
            "infos": 0
          }
        },
        {
          "name": "wp_weather_condition",
          "title": "WeProov condition",
          "position": {
            "items": 0,
            "infos": 1
          }
        },
        {
          "name": "interior_condition",
          "title": "State of exterior cleanliness",
          "position": {
            "items": 0,
            "infos": 2
          }
        },
        {
          "name": "vehicle_color",
          "title": "Colour",
          "position": {
            "items": 0,
            "infos": 3
          }
        }
      ],
      "supports": [
        {
          "name": "rental_contract",
          "title": "Rental Contract",
          "position": {
            "items": 0,
            "supports": 0
          }
        },
        {
          "name": "condition_report_paper",
          "title": "Paper Vehicle Condition Report",
          "position": {
            "items": 0,
            "supports": 1
          }
        },
        {
          "name": "written_proof_picture",
          "title": "Written Proof picture",
          "position": {
            "items": 0,
            "supports": 2
          }
        },
        {
          "name": "other_document",
          "title": "Other document",
          "position": {
            "items": 0,
            "supports": 3
          }
        }
      ],
      "checklists": [
        {
          "name": "ac_tested",
          "title": "A/C Tested",
          "value": false,
          "dropoff_value": false,
          "position": {
            "items": 0,
            "checklists": 0
          }
        },
        {
          "name": "keys_tested",
          "title": "Key(s) tested ?",
          "value": false,
          "dropoff_value": false,
          "position": {
            "items": 0,
            "checklists": 1
          }
        },
        {
          "name": "number_keys",
          "title": "Number of given keys",
          "position": {
            "items": 0,
            "checklists": 2
          }
        }
      ],
      "position": {
        "items": 0
      },
      "process": []
    }
  ]
}
```

## RECUPERER UN WEPROOV

Je viens de finaliser le proovcode 8RWQ33 à partir de l'application.
Maintenant dans l'api pour le récupérer j’ai plus qu'à faire un get avec le paramètre proov_code.
Je rajoute le paramètre lang=fr pour le récupérer tous les titres en français.

# Request 

```
curl -H "Content-Type: application/json" \
	-H "Authorization: Bearer <ACCESS_TOKEN>" \
	-X GET \
	https://api.weproov.com/v1/weproov?proov_code="8RWQ33"&lang=fr
```

# Réponse 

```
{
  "title": "ÉTAT DES LIEUX CERTIFIÉ",
  "description": "Je réalise l'état des lieux au moment de ma prise de poste.",
  "finished_at": "2016-09-22T12:14:03.000Z",
  "proov_code": "8RWQ33",
  "state": "dropoff",
  "template": 218,
  "pdf": <URL DU PDF>,
  "parts": [
    {
      "title": "Locataire",
      "infos": [
        {
          "name": "company_name",
          "title": "Nom de la Société",
          "value": "ProovGroup",
          "position": {
            "parts": 0,
            "infos": 0
          }
        }
      ],
      "supports": [],
      "checklists": [],
      "position": {
        "parts": 0
      }
    },
    {
      "title": "NOT TRANSALTION",
      "infos": [
        {
          "name": "email",
          "title": "Email",
          "value": "Jean-luc@weproov.com",
          "position": {
            "parts": 1,
            "infos": 0
          }
        },
        {
          "name": "name",
          "title": "Nom",
          "value": "Craig",
          "position": {
            "parts": 1,
            "infos": 1
          }
        },
        {
          "name": "first_name",
          "title": "Prénom",
          "value": "Daniel",
          "position": {
            "parts": 1,
            "infos": 2
          }
        },
        {
          "name": "phone_number",
          "title": "Téléphone mobile",
          "value": "0101010101",
          "position": {
            "parts": 1,
            "infos": 3
          }
        }
      ],
      "supports": [],
      "checklists": [],
      "position": {
        "parts": 1
      }
    }
  ],
  "items": [
    {
      "title": "Bien",
      "infos": [
        {
          "name": "register",
          "title": "Immatriculation",
          "value": "AA-BB-CCC",
          "position": {
            "items": 0,
            "infos": 0
          }
        },
        {
          "name": "wp_weather_condition",
          "title": "Condition du WeProov",
          "value": "Nuit",
          "position": {
            "items": 0,
            "infos": 1
          }
        },
        {
          "name": "interior_condition",
          "title": "Etat de proprété intérieur",
          "value": "Moyen",
          "position": {
            "items": 0,
            "infos": 2
          }
        },
        {
          "name": "vehicle_color",
          "title": "Couleur",
          "value": "Bleux",
          "position": {
            "items": 0,
            "infos": 3
          }
        }
      ],
      "supports": [
        {
          "name": "other_document",
          "title": "Autre document",
          "position": {
            "items": 0,
            "supports": 0
          }
        },
        {
          "name": "condition_report_paper",
          "title": "État des lieux papiers",
          "position": {
            "items": 0,
            "supports": 1
          },
          "url": <URL DE L'IMAGE>,
        },
        {
          "name": "rental_contract",
          "title": "Contrat de location",
          "position": {
            "items": 0,
            "supports": 2
          },
          "url": <URL DE L'IMAGE>,
        },
        {
          "name": "written_proof_picture",
          "title": "Justificatif divers",
          "position": {
            "items": 0,
            "supports": 3
          },
          "url": <URL DE L'IMAGE>,
        }
      ],
      "checklists": [
        {
          "name": "ac_tested",
          "title": "Climatisation testée ?",
          "value": true,
          "dropoff_value": false,
          "position": {
            "items": 0,
            "checklists": 0
          }
        },
        {
          "name": "keys_tested",
          "title": "Clé(s) testée(s) ?",
          "value": true,
          "dropoff_value": false,
          "position": {
            "items": 0,
            "checklists": 1
          }
        },
        {
          "name": "number_keys",
          "title": "Nombre de clefs confiée(s)",
          "value": 2,
          "position": {
            "items": 0,
            "checklists": 2
          }
        }
      ],
      "position": {
        "items": 0
      },
      "process": [
        {
          "name": "reading_dashboard_info",
          "title": "Compteurs d'informations (contact mis)",
          "position": {
            "items": "0",
            "process": "0"
          },
          "url": <URL DE L'IMAGE>,
        }
      ]
    }
  ],
  "geoloc": {
    "full_address": "28 Rue Bernard Jugault, 92600 Asnières-sur-Seine, France",
    "longitude": 2.283725,
    "latitude": 48.9103
  }
}
```

