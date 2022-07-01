# Critical rendering path

HTML render on read -> DFS

async js -> concurrent

# CDN

Block direct server access to make other server return the result

support caching

# Flow

1. DNS Resolving -> IP

2. Routing to get path to IP

3.

# Multiplexing

> HTTP 1.1 vs HTTP.2

mutliple TCP connection vs 1 TCP connection

> Chorme use HTTP.2 but create 4 connections

# How server side rendering handle interaction before js compile

## WebVital and LightHouse

- LCP : Largest Contentful Paint
- FID : First Input Delay
- CLS : Cumulative Layout Shift

# Keywords

- DNS optimizing -> initial resolve
- optimize SSR
- Reduce image size
- lazy load
- inline base64 image -> work best for small image
- CSS splitting + inline css when server rendering
- Event re-play -> SERVER side rendering for faster content display
  caching the user event and handle when JS ready
- Re-arrange CSS BLOCK
