# Flows

For default create, read, update & delete operations see [CRUD](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md).
Everything concerning flow executions can be found [here](/2.%20Flow%20runs).


#### GET /api/v1/flows/callback/{callbackId}
Can be used to check whether callbackId is handled.

#### POST /api/v1/flows/callback/{callbackId}
Can be used to resume flows executions. Body can by anything depending on what the flow execution needs.

#### POST /api/v1/flows/executions/{execution}/state
Update the state of an execution. Used to save user input as draft.

<table>
<tr><th>Body</th><th>Description</th></tr>
<tr><td>model</td><td>Can be any object, used to save the current form state.</td></tr>
<tr><td>uuid</td><td>A unique identifier used to point to this state.</td></tr>
</table>

#### GET /api/v1/flows/executions/{executionId}/status
Find out the status of an existing execution with all its details.

<table>
<tr><th>Query parameters</th><th>Description</th></tr>
<tr><td>executionId</td><td>The id of the flow execution</td></tr>
<tr><td>output</td><td>The id or name of the flow output to include in the result. When nothing specified, 
all outputs will be returned.</td></tr>
</table>

#### GET /api/v1/flows/steps
Gets all licensed steps. This is mostly used by the flow builder.

#### GET /api/v1/flows/steps/{step}
Gets the definition of a single step. 

#### POST /api/v1/flows/steps/{step}
To be implemented

#### POST /api/v1/flows/{flow}/contract
To be implemented