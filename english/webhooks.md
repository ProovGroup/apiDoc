## Webhooks

Webhooks can be managed on the plateform in **account** -> **Manage Webhook**

All webhooks make a *post* request with a *body* containing a [Structure WeProov]()

Les réponses doivent être formatées en json.
Elles peuvent contenir :

- A **custom_ref** *string* -> Update the report reference, if it is there.
- A **auto_restart** *boolean*

Be careful, webhooks are randomly called. The last value only will be considered.

### Event type 

#### The initiation

The event is used when initiating a report.

#### Dropoff

The event is used when a report switches from pending to dropoff.

#### Finished

The event is used when a report switches from pending to finished or from dropoff to finished.
