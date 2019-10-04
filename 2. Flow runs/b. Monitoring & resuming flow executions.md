# Monitoring flow executions

Before you start, make sure you are [authenticated](/1.%20Authentication/Authentication.md).

### Get current progress 

##### GET /api/v1/flows/executions/{id}/progress
When a flow is started, among others, an id is returned. Use this id to retrieve progress of this flow execution. 
This will result in a response like:

```{
    "id": "85f8fe94-6f61-4216-af6c-4889e2547b72",
    "percentage": 30,
    "message": "Generating Document",
    "status": "Running",
    "schema": {
        ...
    },
    "model": {
        ...
    },
    "form": [
        ...
    ]
}
```
There are total of 9 states in which a flow progress can be: Success, Warning, Error, Interrupted, Canceled, 
Running, Waiting, Queued & UserInput.

**Success**: Flow has succesfully finished

**Warning**: Flow has finished, something has gone wrong. This happens when a post processing block a has 
failed or a try-catch block has triggered it's catch.

**Error**: Flow could not end. The flow should probably be reconfigured.

**Interrupted**: Flow has been stopped since it has been ongoing for too long.

**Canceled**: Flow has been stopped by the user.

**Running**: Flow is busy.

**Waiting**: Flow is waiting for an exteral event e.g. waiting for people to sign the document using an 
Esign connector.

**Queued**: Flow has not been started yet. Server is waiting for other flows to finish.

**User Input**: Flow is waiting for a user to fill some form data.

### Cancel flow
##### DELETE /api/v1/flows/executions/{id}
<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>id</td><td>The id returned by the initial progress</td></tr>
</table>

### Send user input
##### POST /api/v1/flows/executions/{id}/progress
<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>id</td><td>The id returned by the initial progress</td></tr>
</table>

If the flow is stuck in userinput, it needs form data before it can be continued. It is recommended to use the 
Flow execution panel for this.

To continue a flow, checkout the schema-property in the progress. This contains properties. These properties can be used to construct the POST request.
```
{
   
    "schema": {
        "properties": {
            "ea75ddfd-38f7-4b97-bcc9-3f1756c5d6ff_1cd79690-ade5-41d5-873e-739297926ee9": {
                "type": "string"
            },
        ...

```
In the form property of the progress, you can find how it should be displayed.
```
"form": [
        {
            "htmlClass": "bl-1 bt-1 px-3 pt-2 border-gray-3",
            "items": [
                {
                    "description": "",
                    "key": "ea75ddfd-38f7-4b97-bcc9-3f1756c5d6ff_f706405c-ba8f-46e9-b863-b4cd08aa6ef6",
                    "title": "1",
                    "type": "Enter some text here"
                },
        ...
```
The model property gives default values for this field.
The request POST body can be constructed with the "key" of the field with it's value, in JSON format:
```
{
    "ea75ddfd-38f7-4b97-bcc9-3f1756c5d6ff_f706405c-ba8f-46e9-b863-b4cd08aa6ef6": "Some value entered by the user",
    "...": "...",
    ...
}
```

Make sure all properties in the progress get their value, those who are not entered will be left empty. Once the progress is send, the flow will be resumed.

### Get execution details
##### GET /api/v1/flows/executions/{executionId}
<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>id</td><td>The id returned by the initial progress</td></tr>
</table>

Especially used for debugging flows.

### Get flow output
##### GET /api/v1/flows/executions/{id}/progress
<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>id</td><td>The id returned by the initial progress</td></tr>
</table>

When the flow has ended, there are possibly documents you want to retrieve. The id of the document can be found in the "model" property of the response.
Depending on block of origin, it will be nested in the json-response. The name of the property will not always be "document" but its type will.

```
{
    "model": {
        "B407de9e4_f9e8_47b8_9131_0fa252430a9e": { 
            "document": { 
                "id":"23639cf9-908a-453c-9bbc-f9bb22be9d54",
                "displayName":"My document",
                "type":"document"}
            }
        }
    ,...
}
```

##### GET /api/v1/documents/content/{documentId}
The documentId can be used to fetch the binary document content.


Next [Extras](c.%20Extras.md).
