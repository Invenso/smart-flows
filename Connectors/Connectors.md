#Connector

For default create, read, update & delete operations see [CRUD](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md).

### Connector setup
Before calling the setup on a connector, it has to be created. Use it's id to start the setup process.

A basic setup step looks like this:
```
{
	"id": "1",
	"title": "Setup step title",
	"description": "Setup step description",
	"model": { /* (Default) values for the form */},
	"form": [/* Rendering of the form */],
	"schema": { /* Definition of the model: validators, types etc. Also used by the form.*/},
	"hasNext": true,
	"hasPrevious": false,
	"canFinish": false
}
```
#### POST /api/v1/connectors/{connectorId}/setup
Call this with an empty body since nothing is known yet. Returns a setup step like described above.
#### GET /api/v1/connectors/{connectorId}/setup/current
Get the current step of the setup. Returns a setup step like described above.
#### POST /api/v1/connectors/{connectorId}/setup/cancel
Cancels the setup.
#### POST /api/v1/connectors/{connectorId}/setup/next
if the return body contains <i>hasNext: true</i>, then this endpoint can be called to continue the setup.
The POST-body requires the model parameter of the input combined with the values of the rendered form.
Returns a setup step like described above.
#### POST /api/v1/connectors/{connectorId}/setup/previous
if the return body contains <i>hasPrevious: true</i>, then this endpoint can be called to continue the setup.
The body should be left empty. Returns a setup step like described above.
#### POST /api/v1/connectors/{connectorId}/setup/finish
if the return body contains <i>canFinish: true</i>, then this endpoint can be called to continue the setup. 
The body should be left empty. This returns the connector details.

### Connector types

#### GET /api/v1/connectors/types
Returns all licensed connector types

#### GET /api/v1/connectors/types/{connectorTypeId}
Returns one licensed connector types by id


###Other

#### GET /api/v1/connectors/{connectorId}/test
Test a connector by id. This tells you whether this connector is still valid and can be used in data 
sets/templates/flows.

#### POST /api/v1/connectors/{connectorId}/refresh
Clear the connector cache. The body is ignored.

