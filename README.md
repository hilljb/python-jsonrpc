python-jsonrpc
==============

An asynchronous Twisted (currently TCP-only) JSON-RPC server and client implementation for Python.

Requirements
------------

The only real requirement is Twisted. On Debian-based systems (e.g., Mint or Ubuntu) the repository
package is probably named **python-twisted**, while on OpenSUSE and others you'll find it named
**python-Twisted**.

Additionally, the **simplejson** Python module is recommended. When this is not found, the standard
**json** Python module will be loaded. The simplejson module provides a better implementation of
json in Python and is considerably faster at the time this was written.
