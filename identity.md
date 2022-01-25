# Identity

There are 2 primary types of identities, Flash and Standard.
Flash identities have a short lived fingerprint and ip address. They allow a user to reset all related browsing and tracking data, as well as their ip address and even location in a few seconds.
Standard identities are long lived and their fingerprint is fixed. If there is an issue with their proxy it can be replaced but takes a minute or more rather than seconds. Generally, polling the identity is required to determine when the identity is available again.

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
      "description": "get a list of identities"
    },
    {
      "path": "/?uid=<uid>",
      "method": "get",
      "description": "get a list of identities for a child user"
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
    {
      "path": "/:id/flash",
      "method": "post",
      "description": "get a new proxy container and ip address for a flash identity"
    },
    {
      "path": "/:id/refresh",
      "method": "post",
      "description": "get a new proxy container and ip address for a standard identity"
    }
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
    "enum": ["Standard", "Flash"]
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
    "type": "string",
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
  "users_read_permissions": {
    "type": "string",
    "default": "",
    "description": "a comma separated string of child uids that can access the identity"
  },
  "users_write_permissions": {
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
    "description": "A comma separated list of websites to be added to the allowList"
  },
  "allowListRemove": {
    "type": "string",
    "description": "A comma separated list of websites to be removed from the allowList"
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
