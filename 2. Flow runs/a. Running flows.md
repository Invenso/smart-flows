# Running flows

Before you start, make sure you are authenticated. Start with [Authentication](/1.%20Authentication/Authentication.md).

There are 3 ways to run a flow:
1. Without body
2. With XML as body
3. From a plug-in

Depending on the license, these types are restricted. They can be set using the flow builder.

### POST /api/v1/flows/executions

##### Without body
"flowId": as a query parameter, this should be a flow which does not contain primary entity.

Body: Empty, contents will be ignored.


##### With XML as body
"flowId": as a query parameter, this should be a flow which is based on a template with a schema dataset.

Body: Should contain the XML according to the dataset for the primary template


##### Called from a plug-in (Dynamics or Sugar)
*Should not be called using the API*

"flowId": as a query parameter, this should be a flow which does not contain
 primary entity. This can be forced on any flow by changing the input type of the flow in the flow builder.

"datasetId": as a query parameter, this id is unique for every plugin.

Body: Should contains json according to the following structure

```
{
"id": ["XXXX"],
"entity": "account",
"userId": "XXXX",
"organizationUniqueName": "organizationName"
}
```
"id": The ids of the records, this is an array so multiple values are allowed

"entity": The type of the records

"userId": The id of the user in the plug-in, user should be synced.

"organizationUniqueName": optional


The first response will always be something like:
```
{
  "id":"6de9206a-de42-4182-8f86-a9a8d29fbd56",
  "percentage":0,
  "message":"Generate document",
  "status":"Running"
}
```


### POST /api/v1/flows/executions/start
Variant on the previous call. This one skips all user input and can be used on all types of flow input.
For custom data sets, it will use the default value. The same goes for Smart Forms and user editable fields.

Next [Monitoring flows](b.%20Monitoring%20flow%20executions.md).