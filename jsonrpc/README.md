
Specification
-------------

The JSON-RPC implementation of this module follows the specification for JSON-RPC 2.0 found at
[www.jsonrpc.org/specification](http://www.jsonrpc.org/specification).


### Specification Notes

Keep in mind that JSON has four primitive types (strings, numbers, Booleans, and Null) and two
structured types (objects and arrays). As such, these are the only types possible for values in the
JSON-RPC spec.

### Request Object

An rpc request (client to server) object has the following members.

**jsonrpc** A string representing version of the JSON-RPC protocol being used. This module will use
"2.0" for this value. 
