# Running flows

Before you start, make sure you are authenticated. Start with [Authentication](/1.%20Authentication/Authentication.md).

There are 3 ways to run a flow:
1. Without body
2. With XML as body
3. From a plug-in

Depending on the license, these types are restricted. They can be set using the flow builder.

### POST /api/v1/flows/executions

#### Without body
<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>flowId</td><td>This should be a flow which does not contain primary entity.</td></tr>
</table>


#### With XML as body
<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>flowId</td><td>This should be a flow which is based on a template with a schema dataset.</td></tr>
</table>

The POST-body should contain the XML according to the dataset for the primary template


#### Called from a plug-in (Dynamics or Sugar)
<i>Should not be called using the API</i>

<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>flowId</td><td>This should be a flow which does not contain primary entity. This can be forced on any flow by changing the input type of the flow in the flow builder.</td></tr>
<tr><td>datasetId</td><td>This id is unique for every plugin</td></tr>
</table>

Post body:

```
{
"id": ["XXXX"],
"entity": "account",
"userId": "XXXX",
"organizationUniqueName": "organizationName"
}
```

<table>
<tr><th>POST body</th><th>Description</th></tr>
<tr><td>id</td><td>The ids of the records, this is an array so multiple values are allowed</td></tr>
<tr><td>entity</td><td> show the list of methods which are allowed to log in.</td></tr>
<tr><td>userId</td><td>The id of the user in the plug-in, user should be synced.</td></tr>
<tr><td>organizationUniqueName</td><td>optional</td></tr>
</table>

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