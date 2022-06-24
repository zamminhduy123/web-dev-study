# Worker

## why ?

### Google - RAIL performance model

> Trick - useSetTimeout(0) to bring sync code to async code

## What is ?

Each thread is a JS Engine, each has its own event loop
Each thread is distiguish from each other

### Use SharedArrayBuffer + Atomic to mimic regurlar multithreading

But sharedArrayBuffer not supported in primitive type -> hard to use

Use WebAssembly to convert everything to ShareArrayBuffer

## Downside

1. bring sync to async
2. cloned data is expensive
3. work doesn't have web api access
4. use cost
