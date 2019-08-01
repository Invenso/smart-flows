# Users

For default create, read, update & delete operations see [CRUD](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md).
Delete deactivates a user.


#### GET /api/v1/users/{user}/tokens
List all {user} his/her personal access tokens, secrets or keys will not be returned. Personal access tokens
are also known as API keys.

#### POST /api/v1/users/{user}/tokens
Create a personal access token for {user}.

#### DELETE /api/v1/users/{user}/tokens/{token}
Delete personal access token by id.

#### GET /api/v1/users/external
This is a [paged entity](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md). Only GET is supported. It returns synchronized
users.

#### POST /api/v1/users/external
Synchronizes all users with the login connector. It deactivates all users who do not have one of the Xpertdoc
Smart Flows roles and creates/activates users who have one.

#### GET /api/v1/users/me
Returns the current user using the JWT or the API key.