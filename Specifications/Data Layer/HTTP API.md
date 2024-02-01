# HTTP API Access
Zenea Data Layer servers can choose to provide access to their data or relay requests to connected servers via an HTTP API. Such an API should provide access to a set of functions as listed below.

| HTTP request | Description | Appropriate response body | Possible status codes |
| ---- | ---- | ---- | ---- |
| GET `/blocks` | Requests a list of all the block IDs that the server knows of and that are accessible to it. A server may choose, for reasons of either privacy or performance, to limit the selection of blocks it tells a client about. | the comma-separated block IDs | `400` - OK<br>`500` - Internal Error |
| GET `/block/<BlockID>` | Requests the content of a block by its ID (`<BlockID>`). | the content of the requested block, in binary form | `200` - OK<br>`400` - Bad Request<br>`404` - Not Found<br>`500` - Internal Error |
| POST `/block` | Requests the uploading of a block's contents which are the request body. | the ID of the uploaded block | `200` - OK<br>`400` - Bad Request<br>`403` - Forbidden<br>`500` - Internal Error<br>`502` - Unavailable |
