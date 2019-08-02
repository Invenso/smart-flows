# Flows - in depth

This will explain in a more detailed way how flows are constructed. We will discuss the 
non-standard properties, of which the largest will be the "body"-parameter.


#### Type
This can be simple or advanced. Simple flows have some basic error handling, meaning
postprocessing steps which fail won't always stop the flow. It is recommended to put only one
block in each zone. The Flow Builder in the Project console also restricts the type of flow
steps added to the preZones & postZones (zones before & after the primary generate document step).


#### Input
The type of input for the flow. How is the flow started? It has 3 types: 

- plugin (Dynamics 365 & Sugar): The data set for type plugin can be any of <b>GET /api/v1/datasets/plugin</b>.
- user: The data set can be any schema data set.
- none: The flow does not need any data to start.

Id will be filled on creation & displayName is recommended to be the displayName of the data set.

#### Outputs
Outputs can be configures based on a data set.

#### Settings

#### Body

postProcessingSteps


Simple <-> Advanced

inputBlock
preZones
genDocZone
postZones




Flow steps

Flow blocks

Flow zones

Flow 