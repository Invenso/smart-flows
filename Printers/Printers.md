# Printers

For default create, read, update & delete operations see [CRUD](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md).

#### POST /api/v1/printers/{printer}/test
Send a test document to the printer

#### GET /api/v1/printers/default
Returns the default printer.

#### PUT /api/v1/printers/default
Sets the default printer with a Printer object as POST-body.