# Identity
Identities are the primary resource is the MirageID system. This API allows identities to be managed.

## Routes

```json
{
  "basePath": "identities",
  "routes": [
    {
      "path": "/",
      "method": "post",
      "description": "Create an identity"
    },
    {
      "path": "/",
      "method": "get",
      "description": "Get a list of identities",
      "searchParams": [
        {
          "key": "uid",
          "description": "The value should be the uid of a child user. Using this in the search string will return the subset of identities that the child user has permissions to access",
          "example": "?uid=o3TV1gGIukQteDEom43B9WjSpj93"
        }
      ]
    },
    {
      "path": "/:id",
      "method": "delete",
      "description": "Delete an identity"
    },
    {
      "path": "/:id",
      "method": "put",
      "description": "Update an identity"
    },
    {
      "path": "/:id",
      "method": "get",
      "description": "Get a single identity by id"
    },
  ]
}
```

## Schema

```json
{
  "id": {
    "type": "string",
    "readOnly": true
  },
  "name": {
    "type": "string",
    "required": true
  },
  "type": {
    "type": "string",
    "required": true,
    "enum": ["Standard"]
  },
  "region": {
    "type": "string",
    "enum": [
      "nyc1",
      "sfo1",
      "nyc2",
      "ams2",
      "sgp1",
      "lon1",
      "nyc3",
      "ams3",
      "fra1",
      "tor1",
      "sfo2",
      "blr1",
      "sfo3"
    ],
    "required": true
  },
  "createdAt": {
    "type": "string",
    "readOnly": true
  },
  "createdBy": {
    "type": "string",
    "readOnly": true
  },
  "userId": {
    "type": "string",
    "readOnly": true
  },
  "deletedAt": {
    "type": ["string", "boolean"],
    "readOnly": true,
    "default": false
  },
  "ip": {
    "type": "string",
    "readOnly": true,
    "default": false
  },
  "status": {
    "type": "string",
    "enum": ["removed", "success", "pending"],
    "default": "pending"
  },
  "clearHistory": {
    "type": "boolean",
    "default": false,
    "description": "Whether a flash identity should clear it's history when flashing"
  },
  "autoSyncCookies": {
    "type": "boolean",
    "default": false,
    "description": "Whether to sync cookies between instances of the same identity"
  },
  "creatingBackups": {
    "type": "boolean",
    "default": false,
    "readOnly": true
  },
  "usersReadPermissions": {
    "type": "string",
    "default": "",
    "description": "a comma separated string of child uids that can access the identity"
  },
  "usersWritePermissions": {
    "type": "string",
    "default": "",
    "description": "a comma separated string of child uids that can edit the identity"
  },
  "enableAllowList": {
    "type": "boolean",
    "default": false,
    "description": "Whether the websites that can be used with a given identity is strictly limited"
  },
  "allowList": {
    "type": "string",
    "default": "",
    "immutable": true,
    "description": "the list of websites allowed"
  },
  "allowListAdd": {
    "type": "string",
    "description": "A comma separated list of websites to be added to the allowList",
    "readable": false
  },
  "allowListRemove": {
    "type": "string",
    "description": "A comma separated list of websites to be removed from the allowList",
    "readable": false
  }
}
```

## Available Regions

```json
[
  { "name": "New York 1", "slug": "nyc1" },
  { "name": "San Francisco 1", "slug": "sfo1" },
  { "name": "New York 2", "slug": "nyc2" },
  { "name": "Amsterdam 2", "slug": "ams2" },
  { "name": "Singapore 1", "slug": "sgp1" },
  { "name": "London 1", "slug": "lon1" },
  { "name": "New York 3", "slug": "nyc3" },
  { "name": "Amsterdam 3", "slug": "ams3" },
  { "name": "Frankfurt 1", "slug": "fra1" },
  { "name": "Toronto 1", "slug": "tor1" },
  { "name": "San Francisco 2", "slug": "sfo2" },
  { "name": "Bangalore 1", "slug": "blr1" },
  { "name": "San Francisco 3", "slug": "sfo3" }
]
```
