## Routes
```json
{
  "basePath": "users",
  "routes": [
    {
      "path": "/",
      "method": "get",
      "description": "Get the current user record",
    },
    {
      "path": "/children/:id",
      "method": "delete",
      "description": "Delete a child user",
    },
    {
      "path": "/children",
      "method": "post",
      "description": "Create a child user",
    },
    {
      "path": "/children",
      "method": "get",
      "description": "Get a list of child users",
    },
    {
      "path": "/identity_permissions",
      "method": "post",
      "description": "update the list of users that can access/edit an identity",
    },
    {
      "path": "/:uid",
      "method": "put",
      "description": "update a user by uid, can be used to update a child user",
    },
  ],
}
```
## Schema
```json
{
  "uid": {
    "type": "string",
    "readOnly": true,
  },
  "email": {
    "type": "string",
    "required": true,
    "immutable": true,
  },
  "createdAt": {
    "type": "string",
    "readOnly": true,
  },
  "permissions": {
    "type": "object",
    // this field is only applicable to child users
    "default": {
        "identity": {
          "write": false,
        },
        "identities": false,
        // Example
        // {
        //   '-LxvqfQ6rqXyetGCYLQk': {
        //     read: true,
        //     write: true,
        //   },
        // }
        "user": {
          "read": false,
          "write": false,
        },
        "passwordManager": {
          "write": false,
        },
      }
    },
  "deleted": {
    "type": ["number", "boolean"],
    "default": false,
    "readOnly": true,
  },
  "status": {
    "type": "string",
    "enum": ["active", "trial", "disabled", "deleted"],
    "readOnly": true,
  },
}
```