# Error vs Exception

An **error** is when something wrong or invalid happens in the code. It can cause a memory error, it is something that should never happen and can't be treated.

Whereas an exception throws something when certain conditions are met in the code. It may not correspond to a real error.

**In Javascript**, Errors and Exceptions are syntactically synonymous in JavaScript. The language only implements the Error keyword (through window.Error). You may define custom errors, using the Error.constructor, which takes name and message as parameters.

### Convention

By convention, there is a difference between Error and Exception. An Error indicates a clear violation. A TypeError or ReferenceError means you are not following the language specs.

An Exception is thrown when you access an XMLHttpRequest response before it is complete. Error is a "you broke the law" shout and Exception is an "Almost there!" pad on the shoulder.

# Stale Closure

A closure resembles more a **snapshot 📸 of the scope's data** when the function is created.

This means that there's a risk of accessing **outdated data** given the right circumstances.
