## Routes
```json
{
  "basePath": "identities",
  "routes": [
    {
      "path": "/",
      "method": "post",
      "description": "Create an identity",
    },
    {
      "path": "/",
      "method": "get",
      "description": "get a list of identities",
    },
    {
      "path": "/?uid=<uid>",
      "method": "get",
      "description": "get a list of identities for a child user",
    },
    {
      "path": "/:id",
      "method": "delete",
      "description": "Delete an identity",
    },
    {
      "path": "/:id",
      "method": "put",
      "description": "Update an identity",
    },
    {
      "path": "/regions",
      "method": "get",
      "description": "get a list of supported identity regions",
    },
    {
      "path": "/:id",
      "method": "get",
      "description": "Get a single identity by id",
    },
    {
      "path": "/:id/flash",
      "method": "post",
      "description": "get a new proxy container and ip address for a flash identity",
    },
    {
      "path": "/:id/refresh",
      "method": "post",
      "description": "get a new proxy container and ip address for a standard identity",
    },
    {
      "path": "/:id/backupRegions",
      "method": "put",
      "description": "Change the list of regions for a flash identity",
    },
    {
      "path": "/:id/backupRegionsComplete",
      "method": "get",
      "description": "Check if all backups are finished creating for a flash identity",
    },
  ],
}
```
## Schema
```json
{
  "id": {
    "type": "string",
    "readOnly": true,
  },
  "name": {
    "type": "string",
    "required": true,
  },
  "type": {
    "type": "string",
    "required": true,
    "enum": ["Standard", "Flash"],
  },
  "region": {
    "type": "string",
    "required": true,
  },
  "createdAt": {
    "type": "string",
    "readOnly": true,
  },
  "createdBy": {
    "type": "string",
    "readOnly": true,
  },
  "userId": {
    "type": "string",
    "readOnly": true,
  },
  "deletedAt": {
    "type": "string",
    "readOnly": true,
    "default": false,
  },
  "ip": {
    "type": "string",
    "readOnly": true,
    "default": false,
  },
  "status": {
    "type": "string",
    "enum": ["removed", "success", "pending"],
    "default": "pending",
  },
  "clearHistory": {
    "type": "boolean",
    "default": false,
  },
  "autoSyncCookies": {
    "type": "boolean",
    "default": false,
  },
  "creatingBackups": {
    "type": "boolean",
    "default": false,
    "readOnly": true,
  },
  "users_read_permissions": {
    "type": "string",
    "default": "",
  },
  "users_write_permissions": {
    "type": "string",
    "default": "",
  },
  "enableAllowList": {
    "type": "boolean",
    "default": false,
  },
  "allowList": {
    "type": "string",
    "default": "",
    "immutable": true,
  },
  "allowListAdd": {
    "type": "string",
  },
  "allowListRemove": {
    "type": "string",
  },
}
```
