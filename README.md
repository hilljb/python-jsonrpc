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

Background and Design
---------------------

I'm finding [http://en.wikipedia.org/wiki/JSON-RPC](JSON-RPC) implementations to be a bit
frustrating in the following ways:

1. They tend to assume that the person/coder implementing a server or client is also implementing
the other end of the communication chain. But, what if you need a client written in Python that
connects to an existing server implementation written in C++?
2. They don't allow for easy configuration of a server or client over TCP. I'm really only
interested in TCP for now, and the lack of clear documentation here is annoying.

The design of this module is one that will allow for easy configuration and setup for JSON-RPC
servers and clients within a more complex environment (e.g., one where other JSON-RPC
implementations are part of the communication network). The goal is to also provide an asynchronous
event-driven and reactor-based framework (so that procedure calls requiring some time don't block
calls that may be returned immediately).

Finally, the module is being released under the [https://www.gnu.org/licenses/lgpl.html](LGPL). The
goal here is to allow the module to be used as a library in proprietary projects while maintaining
the open-source property of the library itself.
