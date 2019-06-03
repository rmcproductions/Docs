# Relationships

The relationship between two user accounts.

<aside class="notice">
Bot accounts cannot use any of the endpoints/won't receive any of the gateway events
listed down below.
</aside>

### Relationship Object

###### Relationship Structure

Field | Type | Description
----- | ---- | -----------
id | snowflake | the user id the relationship corresponds to
type | [relationship type](#relationship-type-object) | type of relationship
user? | [User][user] | the other user in the relationship

### Relationship Type Object

###### Relationship Type Structure

Value | Description
----- | -----------
1 | Friend
2 | Blocked
3 | Incoming Friend Request
4 | Outgoing Friend Request

## REST API

The HTTP endpoints corresponding to relationships.

### Get User Relationships

###### `GET /users/[@me][user]/relationships`

Returns an array of [relationship](#relationship-object) objects for your user account.

### Create User Relationship from Username

###### `POST /users/[@me][user]/relationships`

Creates a relationship with the given user.

###### JSON Parameters

Field | Type | Description
----- | ---- | -----------
username | string | the username of the user
discriminator | string | the discriminator of the user

### Create User Relationship from ID

###### `PUT /users/[@me][user]/relationships/[{user.id}][user]`

Creates a relationship to the user with the given ID. Returns `204` on success.

###### JSON Parameters

Field | Type | Description | Default
----- | ---- | ----------- | -------
type | number | the type of relationship to create | 4

### Remove User Relationship

###### `DELETE /users/[@me][user]/relationships/[{user.id}][user]`

Removes any relationship between you and the user. Returns `204` on success.

### Get Mutual Friends

###### `GET /users/[{user.id}][user]/relationships`

Returns a list of [user objects][user] denoting the mutual friends between you and the
other user.

## Gateway

Gateway events corresponding to relationships.

### `RELATIONSHIP_ADD`

Indicates a new relationship has been created.

Contains a [relationship object](#relationship-object) in the `d` field.

### `RELATIONSHIP_REMOVE`

Indicates a relationship has been destroyed.

Contains a [partial relationship object](#relationship-object) in the `d` field.

[user]: https://discordapp.com/developers/docs/resources/user#user-object
