# what is ?

IndexedDB is a **large-scale object store** built into the browser.

Persistently store the data using key-value pairs.

any JavaScript type including boolean, number, string, undefined, null, date, object, array, regex, blob, and files.

# Why indexedDB?

web applications that can work both online and **offline**.

> Google Docs uses the IndexedDB to store the cached documents

# Databases

- highest level of IndexedDB
- contains one or more object stores.

# Object store

An object store is a bucket that you can use to store the data and associated indexes.

> conceptually equivalent to the tables in SQL

An object store contains the records stored as key-value pairs.

# indexed

- allow query data by the properties of the objects.

For example, if you store the contact information, you may want to create indexes on email, first name, and last name so that you can query the contacts by these properties.

# Basic IndexedDB concepts

- IndexedDB databases store key-value pairs
- IndexedDB is transactional (read/write always happens in a transaction.)
- IndexedDB API is **mostly** asynchronous (uses DOM events to notify you when an operation completes and the result is available)
- IndexedDB is a NoSQL system
- IndexedDB follows the same-origin policy

# Basic IndexedDB operations

1. Opening a connection to a database.
2. Inserting an object into the object store.
3. Reading data from the object store.
4. Using a cursor to iterate over a result set.
5. Deleting an object from the object store.

# Fulltext search - reverse index
