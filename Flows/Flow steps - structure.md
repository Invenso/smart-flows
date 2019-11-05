# Flow steps - structure

Flow steps are essential to all flows. They tell how flow blocks should look and what data it needs. The structure will be explained by analyzing the "Generate document"-step.

Like most entities, the step definition has a displayName, id & description. 
iconClass is used to display the icon in the flowbuilder. 
The group and type are labels to categorize the step definitions.
externalOutputParameters can be set as outputParameters in a flow block.
The primaryParameters is no longer used.

InputForm & inputSchema are used to fill the parameters property of a flow block.

The inputSchema defines how the data should be structured (defines the type of the property).

The inputForm defines how the properties are rendered by the flow builder. It contains 
- title
- description
- htmlClass, bodyClass, childClass
- select, text, password, number,...: which type of (input)fields should be used
- singleValue: whether links should be a singleValue or if multiple links are allowed (e.g. mapping data should only have one mapping while a documentName may have multiple).
- placeholder
- kes: which value of the model is referenced by this inputfield
- complexOnly: linked field only
- readonly
- async: If a dropdown needs asynchronous data
- asyncFilter: If a dropdown needs asynchronous filtering
- allowUserEdit: property is allowed to be set to userEditable
- ...

#### Flow step defintion of the "Generate document"-step

```json

{
        "description": "Generate a document.",
        "displayName": "Generate document",
        "externalOutputParameters": [
            "document",
            "documentName",
            "messages",
            "language"
        ],
        "group": "Document",
        "iconClass": "document",
        "id": "e8848859-f919-3fa0-b23f-82a04d51447a",,
        "primaryParameters": [
            "template"
        ],
        "type": "gendoc"
        "inputForm": [
            {
                "htmlClass": "m-x",
                "items": [
                    {
                        "allowUserEdit": false,
                        "async": true,
                        "asyncFilter": true,
                        "complexOnly": false,
                        "displayProperty": "displayName",
                        "idProperty": "id",
                        "key": "template",
                        "placeholder": "None",
                        "readonly": "$context.primaryGenDoc",
                        "type": "select"
                    },
                    {
                        "dependencies": [
                            "template"
                        ],
                        "items": [
                            {
                                "allowUserEdit": false,
                                "async": true,
                                "asyncFilter": true,
                                "displayProperty": "displayName",
                                "key": "data[]",
                                "placeholder": "No data",
                                "type": "select"
                            }
                        ],
                        "key": "data",
                        "title": "Template data",
                        "type": "data-array"
                    },
                    {
                        "allowUserEdit": true,
                        "async": true,
                        "asyncFilter": true,
                        "complexOnly": false,
                        "displayProperty": "displayName",
                        "idProperty": "id",
                        "key": "language",
                        "placeholder": "Default (English)",
                        "type": "select"
                    }
                ],
                "title": "Basic Settings",
                "titleClass": "h5 bt-1 border-blue-4 text-blue-4 w-100 mt-3",
                "type": "section"
            },
            {
                "htmlClass": "m-x",
                "items": [
                    {
                        "complexOnly": false,
                        "key": "documentName",
                        "placeholder": "Not specified",
                        "singleValue": false,
                        "type": "text"
                    },
                    {
                        "bodyClass": "d-flex justify-content-between",
                        "childClass": "w-45",
                        "items": [
                            {
                                "key": "dateFormat",
                                "placeholder": "Not specified",
                                "titleMap": [
                                    {
                                        "name": "dd-MM-yyyy",
                                        "value": "dd-MM-yyyy"
                                    },
                                    ...
                                ],
                                "type": "select"
                            },
                            {
                                "key": "timeFormat",
                                "placeholder": "Not specified",
                                "titleMap": [
                                    {
                                        "name": "HH:mm",
                                        "value": "HH:mm"
                                    },
                                    ...
                                ],
                                "type": "select"
                            }
                        ],
                        "type": "section"
                    },
                    {
                        "key": "format",
                        "placeholder": "Default value (Word document (*.docx))",
                        "titleMap": [
                            {
                                "name": "Word document (*.docx)",
                                "value": "Docx"
                            },
                           ...
                        ],
                        "type": "select"
                    }
                ],
                "title": "Name & format settings",
                "titleClass": "h5 bt-1 border-blue-4 text-blue-4 w-100 mt-3",
                "type": "section"
            }
        ],
        "inputSchema": {...},
        "outputId": "f7723dc8-445f-33ef-bc14-3fce8c0b2b68",
        "outputSchema": {
            "$schema": "http://json-schema.org/draft-04/schema#",
            "additionalProperties": false,
            "definitions": {
                "DocumentVal": {
                    "additionalProperties": false,
                    "format": "document",
                    "properties": {
                        "displayName": {
                            "type": "string"
                        },
                        "id": {
                            "type": "string"
                        },
                        "type": {
                            "enum": [...],
                            "type": "string"
                        }
                    },
                    "type": "object"
                },
                "LanguageVal": {
                    "additionalProperties": false,
                    "format": "language",
                    "properties": {
                        "displayName": {
                            "type": "string"
                        },
                        "id": {
                            "type": "string"
                        },
                        "type": {
                            "enum": [...],
                            "type": "string"
                        }
                    },
                    "type": "object"
                }
            },
            "properties": {
                "document": {
                    "$ref": "#/definitions/DocumentVal",
                    "description": "The generated document",
                    "title": "Generated document"
                },
                "documentName": {
                    "description": "The name of the document",
                    "title": "Document name",
                    "type": "string"
                },
                "language": {
                    "$ref": "#/definitions/LanguageVal",
                    "description": "The language that is actually used",
                    "title": "Language"
                },
                "messages": {
                    "description": "Messages",
                    "title": "Messages",
                    "type": "string"
                }
            },
            "required": [
                "document"
            ],
            "title": "Generate Document Output",
            "type": "object"
        }
    }
```
