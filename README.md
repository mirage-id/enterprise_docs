# enterprise_api_docs

## Getting Started

### Base URL
The MirageID api is located at:
```
https://api.mirageid.com
```

### Authentication
Once you have created an api token in the account portal, attach it as a header to your request as follows:
```
Authorization: `<api-token>`
```

### Content Type
The following header should be sent with each request:
```
'Content-Type': 'application/json'
```

### Response Schema
Responses from the API will have the following shape:

#### For Create/Update/Get operations

##### For Success Responses
```
{
  status: 'success',
  data: <entity>
}
```

##### For Error Responses
```
{
  status: 'error',
  error: 'string describing error for example "Failed to create an identity"',
}
```

#### For Get operations that return a list
```
{
  status: 'success',
  data: [
    <entity>,
    <entity>,
    <entity>,
  ]
}
```

### Exceptions
Generally, operations on an entity will return the current state of the entity. However, some endpoints have a special use-case that does not comply with the standard schema. To resolve this, their expected response/request schema is noted in the docs.

## Reading the docs
Currently, the API documentation is an excerpt of configuration files used to setup the api. This provides a concise and easy to parse view of the systems operations and schema for a given entity. Below is a general guide of how to interpret the docs:

### Routes
* `basePath` - The prefix for all routes defined for the entity. ex: https://api.mirageid.com/users/
* `routes` - An list of routes available using the `basePath` as a prefix.
  * `path` - The sub-path of `basePath` used to address the endpoint
  * `method` - The required http method
  * `description` - A concise description of the operation performed by a given route

### Schema
The schema describes but the request and response shape of an entity. Some fields are only available in one or the other as described below:
* `<fieldName>` - The name of a fields in the schema
  * `type` - The fields type in javascript. Primitive types are available such as "string", "number", "boolean", etc. "object" can refer to either an array like or dictionary like object. The value of this field can be an array which indicates that more than 1 type is valid. For example: if an identity has not yet been deleted the `deleted` field has a value of `false`, a boolean. Once it is deleted the value will be a unix timestamp which is a number.
  * `readOnly` - A field that is always internally controlled and not part of either a create or update request.
  * `immutable` - A field which can be included in a create request but cannot be changed afterwards
  * `required` - A field that must be included in the body of a `POST` request
  * `enum` - When the value of `type` is "string" this is used to describe a limited set of strings that are valid values
  * `default` - The default value set for a field on create if none if provided