# Flow execution extras

Before you start, make sure you are [authenticated](/1.%20Authentication/Authentication.md).

##### GET /api/v1/flows/{flow}/thumbnail
Get the thumbnail for a flow, this is the thumbnail for primary template of the flow.

##### GET /api/v1/flows/{flow}/executions
Get all executions for one flow

##### GET /api/v1/flows/executions
Get all executions for all flows. This is paged.

##### POST /api/v1/flows/executions/filter
Get all executions for all flows filtered by a complex filter object.

```
{
  "group": {
     "nodes": [
      {
        "condition": {
          "key": "displayName",
          "operator": "equals",
          "values": ["Account"]
        }
      },
      {
        "condition": {
          "key": "createdAt",
          "operator": "lessThanOrEqualTo",
          "values": ["2019-01-01"]
        }
      }
    ],
    "type": "and"
  }
}
```

This request for example will return all flow executions before or ran on 2019-01-01 which ended in status Success or Error.
For more info [see filtering](/3.%20Smart%20Flows%20Entities/2.%20Filtering.md).

##### POST /api/v1/flows/executions/statistics
This needs a similar body like the previous endpoint and returns the data required to draw charts.


Continue with [paging](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md).
