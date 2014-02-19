
Specification
-------------

The implementation of JSON-RPC for this module follows the specification for JSON-RPC 2.0 found at
[www.jsonrpc.org/specification](http://www.jsonrpc.org/specification).


### Specification Notes

Keep in mind that JSON has four primitive types (strings, numbers, Booleans, and Null) and two
structured types (objects and arrays). As such, these are the only types possible for values in the
JSON-RPC spec.

### Request Object

An rpc request (client to server) object has the following members.

**jsonrpc** (required) A string representing version of the JSON-RPC protocol being used. This
module will use "2.0" for this value.

**method** (required) A string containing te name of the method to be called. Note that method names
beginning with 'rpc' followed by a period (U+002E or ASCII 46) are reserved and must not be used.

**params** A JSON structured value (object or array) holding the parameter values to be used during
the invocation of the method. This key/value is not required and may be omitted from the request
JSON string. The parameter structure is specified as follows: When included as a JSON object, the
keys and values must match the possible method option keys expected on the server, including case.
When included as a JSON array, the parameters are a sequence of values expected by the server in
order.

**id** A string or number. (Technically, the spec states that an id can also be a Null value, but
warns against this usage. In addition, an id set to a number can contain fraction parts, but this is
strongly warned against in the spec.) This key/value is not required, but is used to correlate
requests with responses in environments where simultaneous or asynchronous request calls are made.
In this module's implementation, the request JSON-RPC formed by the client cannot use Null id
values. (However, the response JSON-RPC formed by the client can use Null id values and the server
will understand Null if it is received as an id value.)

#### Notifications

When the client wishes to send a notification to the server, a JSON-RPC request may be sent with no
'id' key/value set. The server will not reply to such requests.

### Response Object

Except in the case of notifications (JSON-RPC requests without an id key/value), the server must
send a response. The response is expressed as a single JSON object with the following members.

**jsonrpc** (required) A string representing version of the JSON-RPC protocol being used. This
module will use "2.0" for this value.

**result** (required on success, not used on error) When returned, the value is determined by the
method invoked on the server.

**error** (required on error, not used on success) When returned, the value must be a JSON object
with keys/values as follows..

| **code**         | **message**      | **meaning**                                       |
| ---------------- | ---------------- | ------------------------------------------------- |
| -32700           | parse error      | invalid JSON received by server                   |
| -32600           | invalid request  | JSON request was invalid                          |
| -32601           | method not found | method not found / unavailable                    |
| -32602           | invalid params   | invalid method parameters                         |
| -32603           | internal error   | internal JSON-RPC error                           |
| -32000 to -32099 | server error     | reserved for implementation defined server errors |

For implementation specific errors, the meaning component of the JSON object will return information
about the error.

**id** (required) The value of this is identical to that of the corresponding request call. (See
documentation above.) If there is an error in detecting the id in the request call, the id value in
the response will be set to Null.

### Batch

To send several request calls at the same time, the client may send a JSON array of request objects.

After all requests in the batch call are processed, the server will send a response in the form of a
JSON array of RPC response objects. The sizes of the request and response arrays may be different,
as response objects aren't provided in the case of notification requests. The order of elements in
the arrays may be different and distinct response objects are found via their id key values.

The response object may be a single (non-array) object in the case when the batch request is not
understood. In the case when any request in the batch is itself not understood, the corresponding
error response will be sent for that RPC while result responses may be sent for other RPCs in the
batch.



