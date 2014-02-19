
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

**jsonrpc** (required) A string representing version of the JSON-RPC protocol being used. This module will use
"2.0" for this value.

**method** (required) A string containing te name of the method to be called. Note that method names
beginning with 'rpc' followed by a period (U+002E or ASCII 46) are reserved and must not be used.

**params** A JSON structured value (object or array) holding the parameter values to be used during
the invocation of the method. This key/value is not required and may be omitted from the request
JSON string.

**id** A string or number. (Technically, the spec states that an id can also be a Null value, but
warns against this usage. In addition, an id set to a number can contain fraction parts, but this is
strongly warned against in the spec.) This key/value is not required, but is used to correlate
requests with responses in environments where simultaneous or asynchronous request calls are made.
In this module's implementation, the request JSON-RPC formed by the client cannot use Null id
values. (However, the response JSON-RPC formed by the client can use Null id values and the server
will understand Null if it is received as an id value.)
