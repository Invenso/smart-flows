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
				"id": "4992e88f-0a3b-4b1c-b54d-7f57e04f3491",
				"condition": {
					"key": "status",
					"operator": "in",
					"values": ["Success","Error"]
				}
			},
			{
				"id": "3665a89a-2aac-42dc-b966-01b3106397a8",
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

##### POST /api/v1/flows/executions/statistics
This needs a similar body like the previous endpoint and return the data required to draw charts.
