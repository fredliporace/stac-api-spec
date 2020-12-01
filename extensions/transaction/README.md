# Transaction API Extension

**Extension [Maturity Classification](../README.md#extension-maturity): Pilot**

The core STAC API doesn't support adding, editing, or removing items.
The transaction API extension supports the creation, editing, and deleting of items through POST, PUT, PATCH, and DELETE requests.

STAC Transactions are based on the [OGC API - Features](https://ogcapi.ogc.org/features/) transactions, as 
specified in [Part 4: Simple Transactions](http://docs.opengeospatial.org/DRAFTS/20-002.html). The core
OGC standard lays out the end points for transactions, without specifying any content types. For STAC we
use STAC Items in our transactions, and those transaction must be done at the core OGC API - Features endpoints,
under `/collections/{collectionID}/items`. The OpenAPI document (specified as an OpenAPI fragment that 
gets build in the full STAC OpenAPI document) simply gives the STAC examples of using the
Simple Transactions API mechanism.

OGC Simple Transactions is still a draft standard, so once it is released STAC will align to a released one,
but we anticipate few changes as it is a very simple document.

STAC Transactions additionally support optimistic locking through use of the ETag header, as specified in the
OpenAPI document. This is not currently specified in OGC API - Features, but it is compatible and we will 
work to get it incorporated.

## Methods

| Path                                                   | Content-Type Header | Description |
| ------------------------------------------------------ | ------------------- | ----------- |
| `POST /collections/{collectionID}/items`               | `application/json`  | Adds a new item to a collection. |
| `PUT /collections/{collectionId}/items/{featureId}`    | `application/json`  | Updates an existing item by ID using a complete item description. |
| `PATCH /collections/{collectionId}/items/{featureId}`  | `application/json`  | Updates an existing item by ID using a partial item description, compliant with [RFC 7386](https://tools.ietf.org/html/rfc7386). |
| `DELETE /collections/{collectionID}/items/{featureId}` | n/a                 | Deletes an existing item by ID. |
