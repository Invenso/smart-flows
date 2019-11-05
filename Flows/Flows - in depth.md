# Flows - in depth structure

This will explain in a more detailed way how flows are structured. We will discuss the 
non-standard properties, of which the largest will be the "body"-parameter.


#### Type
This can be simple or advanced. Simple flows have some basic error handling, meaning
postprocessing steps which fail won't always stop the flow. It is recommended to put only one
block in each zone. 

The Flow Builder in the Project console adds some extra restrictions.
- the type of flow steps added to the preZones & postZones (zones before & after the primary generate document step)
- nesting is restricted to one level deep
- one block per zone


#### Input
The type of input for the flow. How is the flow started? It has 3 types: 

- plugin (Dynamics 365 & Sugar): The data set for type plugin can be any of <b>GET /api/v1/datasets/plugin</b>.
- user: The data set can be any schema data set.
- none: The flow does not need any data to start.

Id will be filled on creation & displayName is recommended to be the displayName of the data set.


#### Taggroups
It's possible to add tags to flows (templates & data sets). If configured this way (Control panel, Settings, Tag defaults), some tags will be added on creation.

#### Outputs
Multiple outputs datas can be added & later retrieved by name (or all at once). These are all based on data sets. You can use plugin defined output data sets or any other standard type of data set. Plugin data sets can be retrieve with a GET to "/api/v1/datasets/plugin/output" Fields mapped in this, should have fieldPaths corresponding with fields in the data set. The example at the bottom of this page contains one output with one output mapping defined by a custom data set (type: user).

Once a flow has been finished, the output can be retrieve with GET "/api/v1/flows/executions/{executionId}/status". If no output is specified, all outputs will be returned. The name of the output can be used as a query parameter (in the example: 'output=Output 1').

#### Settings
groupToSingleDocument - Sometimes, you want to merge multiple documents into a single one. This can only be done for the documents created by the primary "Generate document"-step. When set to true and multiple records (Dynamics or Sugar) are used for input, all documents will be generated and merged (preprocessing & generateDocument zones are executed). Thereafter, the postprocessing steps will be executed for the one documents.  

askQuestionsFirst - Upon starting a flow for multiple records, or for a flow which can be paused (e-signing) it can be handy to first ask all user input first. This is not always possible. Asking questions based on conditions can have unexpected results. 

#### Primary Template
A flow always contains at least one "Generate document"-step The template used for this, is the primaryTemplate.

#### Primary Entity
The primary template can have multiple data sets linked to it. In order to know from which entity the flow can be started, it can be necessary to include the primary entity on creation

#### Body
postProcessingSteps - Upon creation, this parameter can be filled by adding postProcessing flow step definitions to it. The id and displayName are enough. Once created, this parameter is ignored.

Note: A flow zone is a logical way of splitting the flow in parts. One zone can contain multiple flow steps. Athough, in standard flows, this is restricted to one.

preZones - This list of zones can be used to collect data or create conditions. In advanced flows, there is no limit to the type of steps you can add to these zones. 
genDocZone - This zone contains the primary "Generate document"-step, by default, its required parameters are filled (data is linked). Only in simple flows other steps can be added to this.
postZones - This list of zones is used to do the post processing step like storing the document in other systems, sending e-mails,... In advanced flows, there are no restrictions. More data can be collected and more documents can be generated.

blocks: A zone contains 0+ blocks, an id and an optional displayName. The id will be generated for you on updating the flow or you can create it yourself.

block:
    step: A block is always based on a step definition or a condition. This is filled if it is based on a step definition
        stepId: The id of the flow step defintion
        userSelectable: Whether the user can choose to execute this step (while runnning)
        userSelectableDefault: The default value for this
        parameters: Depending on the step definition, different parameters will be settable.
    try, switch, condition: The are the control blocks and can have lists of zones of their own
    outputParameters: These are the parameters you want to retrieve when your execution has ended. They can be found in the step  definition
   
##### parameters further explained following the example
The "Generate document"-step has the following parameters: data, dateFormat, documentName, format, language, template and timeFormat.
Let's take a look at the documentName parameter:




#### Example
The following flow contains a "Generate document"-step and a "Store in Sharepoint"-step.

```json
{
    "body": {
        "genDocZone": {
            "blocks": [
                {
                    "displayName": "Generate document",
                    "id": "c35d2742-86f7-4beb-a56f-6964cf7e3749",
                    "outputParameters": [
                        "document"
                    ],
                    "step": {
                        "parameters": {
                            "data": [
                                {
                                    "extendable": false,
                                    "required": false,
                                    "userEditable": false,
                                    "variableValue": [
                                        {
                                            "blockId": "052b823d-8c4a-4ecf-b19e-690bb65eac38",
                                            "displayName": "Data",
                                            "isVariable": true,
                                            "outputId": "a1851858-a4ad-3f4f-9fe5-260e58c347fa",
                                            "parameter": "data"
                                        }
                                    ]
                                }
                            ],
                            "dateFormat": {
                                "extendable": false,
                                "required": false,
                                "userEditable": false
                            },
                            "documentName": {
                                "extendable": false,
                                "required": false,
                                "userEditable": false,
                                "variableValue": [
                                    {
                                        "isVariable": false,
                                        "value": "document for "
                                    },
                                    {
                                        "blockId": "052b823d-8c4a-4ecf-b19e-690bb65eac38",
                                        "dataPath": "account/name",
                                        "displayName": "Account Name",
                                        "isVariable": true,
                                        "outputId": "a1851858-a4ad-3f4f-9fe5-260e58c347fa",
                                        "parameter": "data"
                                    },
                                    {
                                        "isVariable": false,
                                        "value": ""
                                    }
                                ]
                            },
                            "format": {
                                "extendable": false,
                                "required": false,
                                "userEditable": false,
                                "value": "Pdf"
                            },
                            "language": {
                                "extendable": false,
                                "required": false,
                                "userEditable": false
                            },
                            "template": {
                                "extendable": false,
                                "required": false,
                                "userEditable": false,
                                "value": {
                                    "displayName": " Account",
                                    "id": "913534d4-691d-4cdc-8db9-98e2fb21163c",
                                    "type": "template"
                                }
                            },
                            "timeFormat": {
                                "extendable": false,
                                "required": false,
                                "userEditable": false
                            }
                        },
                        "stepId": "e8848859-f919-3fa0-b23f-82a04d51447a"
                    }
                }
            ],
            "id": "7a35402b-7df8-454f-ac8d-a5f027953e2b"
        },
        "postProcessingSteps": [],
        "postZones": [
            {
                "blocks": [
                    {
                        "displayName": "Store in SharePoint",
                        "id": "f0215216-d699-4a70-98fe-ec2d5c484ac2",
                        "outputParameters": [
                            "link",
                            "folderLink"
                        ],
                        "step": {
                            "parameters": {
                                "document": {
                                    "variableValue": [
                                        {
                                            "blockId": "c35d2742-86f7-4beb-a56f-6964cf7e3749",
                                            "displayName": "Generated document",
                                            "isVariable": true,
                                            "outputId": "f7723dc8-445f-33ef-bc14-3fce8c0b2b68",
                                            "parameter": "document"
                                        }
                                    ]
                                }
                            },
                            "stepId": "2dd4fa03-b880-3e8d-b5ce-99737cc9f4f3"
                        }
                    }
                ],
                "id": "485ea935-28da-4eb2-b248-bb3e217b6781"
            }
        ],
        "preZones": [
            {
                "blocks": [
                    {
                        "displayName": "Retrieve Account",
                        "id": "052b823d-8c4a-4ecf-b19e-690bb65eac38",
                        "outputParameters": [],
                        "step": {
                            "parameters": {
                                "dataset": {
                                    "value": {
                                        "displayName": "Account",
                                        "id": "5f1b3d2e-6463-420f-abfd-5b6b2285f1d1",
                                        "type": "dataset"
                                    }
                                },
                                "id": {
                                    "variableValue": [
                                        {
                                            "blockId": "313316e9-c57f-472b-9725-3175f6c09c55",
                                            "dataPath": "DynamicsRequest/id",
                                            "displayName": "Selected record",
                                            "isVariable": true,
                                            "parameter": "data"
                                        }
                                    ]
                                }
                            },
                            "stepId": "ceed64b5-ec90-3c05-8da6-89dbe0ad2b5b"
                        }
                    }
                ],
                "id": "6a273ef0-baf8-4154-9333-43165ef97fd0"
            }
        ]
    },
    "createdAt": "2019-11-05T11:16:34.677Z",
    "createdBy": {
        "displayName": "Admin Aelbrecht",
        "id": "db6a0eb5-0748-425f-82d0-d5dd45de1e3d"
    },
    "description": "This flow is to be started from a Dynamics account",
    "displayName": "Test flow on account",
    "id": "313316e9-c57f-472b-9725-3175f6c09c55",
    "input": {
        "dataset": {
            "displayName": "Dynamics",
            "id": "f23c0d16-f70d-404f-b6fb-347cc7c966a5"
        },
        "displayName": "Dynamics",
        "id": "313316e9-c57f-472b-9725-3175f6c09c55",
        "type": "plugin"
    },
    "modifiedAt": "2019-11-05T11:45:33.541Z",
    "modifiedBy": {
        "displayName": "Admin Aelbrecht",
        "id": "db6a0eb5-0748-425f-82d0-d5dd45de1e3d"
    },
    "outputs": [
        {
            "dataset": {
                "displayName": "Custom 1",
                "id": "ea75ddfd-38f7-4b97-bcc9-3f1756c5d6ff",
                "type": "dataset"
            },
            "description": "",
            "displayName": "Output 1",
            "fieldMap": {
                "fields": [
                    {
                        "fieldPath": "custom_1/_1",
                        "value": [
                            {
                                "isVariable": false,
                                "value": ""
                            },
                            {
                                "blockId": "c35d2742-86f7-4beb-a56f-6964cf7e3749",
                                "displayName": "Document name",
                                "isVariable": true,
                                "outputId": "f7723dc8-445f-33ef-bc14-3fce8c0b2b68",
                                "parameter": "documentName"
                            },
                            {
                                "isVariable": false,
                                "value": ""
                            }
                        ]
                    }
                ]
            },
            "id": "542923bd-46d7-450a-ac94-7e61a8093508",
            "type": "user"
        }
    ],
    "primaryEntity": "account",
    "primaryTemplate": {
        "displayName": " Account",
        "id": "913534d4-691d-4cdc-8db9-98e2fb21163c"
    },
    "settings": {},
    "tagGroups": [
        {
            "group": {
                "displayName": "Availability",
                "id": "1ae5c5b1-742d-4f51-adaa-33295df61c8b"
            },
            "tags": [
                "Flyout"
            ]
        }
    ],
    "type": "simple"
}
```
