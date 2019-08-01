# Dependencies

The dependencies of an object are references toward other objects. Outbound dependencies are needed for the current object. Inbound dependencies are objects which need the current item.

For example a template could have a dataset & a connector as outbound dependency & a flow as inbound dependency.

####GET /api/v1/dependencies/{objectType}/{objectId}
<table><tr><th>Query parameters</th><th>Description</th></tr>
<tr><td>depth</td><td>full or direct</td></tr> 
<tr><td>direction</td><td> inbound (default), outbound or both</td></tr>
</table>

The objectType (camelCased) can be any of the Smart Flows entities [as listed](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md). 
The id must be for an object of the corresponding objectType.
