# User

In the MirageID system there are 2 types of users. Parent users which are account owners and child users which are additional users who's access is limited to the permissions that have been set by the parent user.

## Routes

```json
{
  "basePath": "users",
  "routes": [
    {
      "path": "/",
      "method": "get",
      "description": "Get the current user's record"
    },
    {
      "path": "/:uid",
      "method": "put",
      "description": "update a user by uid, can be used to update a child user"
    }
    {
      "path": "/children/:id",
      "method": "delete",
      "description": "Delete a child user"
    },
    {
      "path": "/children",
      "method": "post",
      "description": "Create a child user"
    },
    {
      "path": "/children",
      "method": "get",
      "description": "Get a list of child users"
    },
        {
      "path": "/children/:uid",
      "method": "get",
      "description": "Get a child user by uid"
    },
        {
      "path": "children/:uid",
      "method": "put",
      "description": "update a child user by uid"
    }
  ]
}
```

## Schema

```json
{
  "uid": {
    "type": "string",
    "readOnly": true
  },
  "email": {
    "type": "string",
    "required": true,
    "immutable": true
  },
  "createdAt": {
    "type": "string",
    "readOnly": true
  },
  "permissions": {
    "type": ["object", "undefined"],
    "default": {
      "identity": {
        "write": false
      },
      "identities": false,
      "user": {
        "read": false,
        "write": false
      },
      "passwordManager": {
        "write": false
      }
    },
  },
  "deletedAt": {
    "type": ["string", "boolean"],
    "readOnly": true,
    "default": false
  },
  "status": {
    "type": "string",
    "enum": ["active", "trial", "disabled", "deleted"],
    "readOnly": true
  },
  "masterPassword": {
    "type": "string",
    "readable": false,
    "description": "Required (and only included) when creating a child user. This is the password for the parent user's account. It is needed to create an encrypted key for the child that is compatible with the parent's"
  }
}
```

### User permission
Child users can be granted fine grained access to the parent user's account and identities.
The `permissions` value only exists on child and not parent users.
All permissions values are booleans.

- `identity` - General identity permissions
  - `write` - `boolean` Whether the user can create identities.

- `identities` - Permissions granted for a specific identity (an object keyed by identity ids)
  - `-LxvqfQ6rqXyetGCYLQk` - The id of the identity
    - `read` - Whether the user can access the identity,
    - `write` - Whether the user can edit the identity,

- `user` - User management permissions
  - `read` - Whether the user can access a list of other child users on the account
  - `write` - Whether the user can create/edit child users on the account

- `passwordManager` - Access to the build in password manager (all users can autofill passwords)
  - `write` - Whether the user can save new passwords to the password manager
