# Process vs Thread

1. process cannot access other process resource, thread can
2. Thread have a differnt stack ? but same heap
3. process A talk to process B through IPC. Thread can maybe communicate using global var
4. Context switching (research)

# Parallel vs Concurrent

without concurrent -> **starvation**

concurrent means that all task can all work seemingly the same time but not parallel but all task must not depend on each other

mix parallel + concurrent -> better

> Block vs NonBlock

# Event Driven - Chrome follow

# Implement Eventloop? libuv

# GC

- clear local scope, reference link

# FileAPI

## Blob

Object contains raw data (Binary)

- **stream**

## File

extends of Blob

> Why File ?

A file is a contractor to Blob, **trust resource** **secured**. User give file -> more trust

## FileReader

read user and return file

### It's important to clean up file

> Can cheat using MIME type
