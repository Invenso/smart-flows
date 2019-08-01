# Data sets

For default create, read, update & delete operations see [CRUD](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md).


#### GET /api/v1/datasets/{datasetId}/data
[See paged entities](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md), does not support update & delete. This can be 
combined with the Data API

#### GET /api/v1/datasets/{datasetId}/entityrefs
Gets entity references to the primary entity of the dataset. This is used to create samples by reference.

#### POST /api/v1/datasets/layout
Gets a list of available entities in the given dataset. The body should contain a dataset.

#### GET /api/v1/datasets/plugin
Gets all input data sets defined by plugins.

#### GET /api/v1/datasets/plugin/output
Gets all output data sets defined by plugins.