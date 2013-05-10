node-lmdb
=========

Node.js binding for lmdb, an extremely fast and lightweight key-value store database.

About this module
-----------------

The aim of this node module is to provide bindings so that people can use lmdb from their node applications, aiming for a simple and clean API which is on par with the lmdb API but tries to apply javascript patterns and naming conventions as much as possible to make users feel familiar about it.

About lmdb
----------

* Key-value store, NoSQL
* In-process, no need to squeeze your data through a socket
* Support for transactions and multiple databases in the same environment
* Support for multi-threaded and multi-process use
* Zero-copy lookup (memory map)
* For more, visit http://symas.com/mdb

Basics
------

LMDB has four different entities:

* `Env` represents a full database environment. The same environment can be used by multiple processes, but a particular `Env` object **must** be used by one process only. You can operate with the same environment from multiple threads.
* `Dbi` represents a sub-database which belongs to a database environment.
* `Txn` represents a transaction. Multiple threads can open transactions for the same `Env`, but a particular `Txn` object **must** only be accessed by one thread, and only one `Txn` object can be used on a thread at a time. (NOTE: The `noTls` option in the environment will change this behaviour for *read-only* transactions, so that a thread can then create any number of *read-only* transactions and any number of threads can access the same *read-only* transaction.) Note that **only one** *write* transaction can be open in an environment in any given time. `env.beginTxn()` will simply block until the previous one is either `commit()`ted or `abort()`ed.
* `Cursor` objects can be used to iterate through multiple keys in the same database.

Here is how you use LMDB in a typical scenario:

* You create an `Env`, configure it for your use case and `open()` it.
* You open a `Dbi` with `env.openDbi()` where you can tell `node-lmdb` how you want to configure your database.
* Now you can create `Txn`s with `env.beginTxn()` and operate on the database with `txn.get()`, `txn.put()` etc.
* When you are done, you should either `abort()` or `commit()` your transactions and `close()` your databases and environment.

Examples
--------

You can find some in the source tree. More will be added later.

Contributing
------------

Feel free to send me pull requests on GitHub. Contributions are more than welcome! :)
