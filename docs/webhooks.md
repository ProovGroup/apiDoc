## Webhooks

les webhooks sont gérées directement sur la platforme dans **compte** -> **gérer les webhooks**

Toutes les webhooks font une requête *post* avec un *body*  contenant une [Structure WeProov]()

Les réponses doivent être formatées en json.
elles peuvent contenir :

- un **custom_ref** *string* -> Update la référence du rapport si elle est présente.
- un **auto_restart** *boolean*

Attention, les webhooks sont appelées dans n'importe quel ordre. Seul la dernière valeur renvoyée sera prise en compte.

### Type d'event 

#### L'init

Cet évènement est utilisé à l'initialisation d'un rapport.

#### Dropoff

Cet évènement est utilisé lorsqu'un rapport passe de l'état pending à l'état dropoff.

#### finished

Cet évènement est utilisé lorsqu'un rapport passe de l'état pending à l'état finished ou de dropoff à finished.
