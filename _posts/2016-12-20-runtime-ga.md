---
layout: post
title:  "Java SDK Runtime GA Plan"
date:   2016-12-20 17:56:00 -0800
author: "Jianghao Lu"
comments: true
---

## Goals to achieve

- [ ] Having RestClient as the center piece, everything except the dependency of OkHttp and Retrofit to be pluggable
- [ ] `restClient.newBuilder().build()` should create a new RestClient with exactly the same behavior with everything copied
- [x] RestClient is immutable except for header and log level
- [ ] Having a protocol interface for every pluggable
- [x] Wrapped logging mechanism complying with slf4j
- [ ] Limit the number of public methods
- [ ] Use unique names over simple names
- [ ] Use more factory methods than constructors
- [ ] Make classes final when possible
- [x] Simplier (de)serializer protocol
- [ ] Simplier response builder protocol
- [ ] Use more composition over inheritance for simpler protocols between runtime and azure runtime
- [ ] Use unchecked exceptions
- [ ] Make strategies stateless and singletons
- [ ] Delcare static on methods that don't access anything in scope
- [ ] Delcare `@throws` and `@since` on methods explicitly

## What is a RestClient supposed to do

### Compositions

**Staticly required:**
- An `OkHttp3` client
- A `Retrofit2` client

n.b. Other than the staticly required dependencies, every other class needs to be either wrapped or adapted.

**Dynamically required:**
- A (de)serializer
- A response builder

**Optional:**
- A `ServiceClientCredentials` (or a better credentials provider in the future)
- Many extra user agent headers
- Many extra interceptors
- Many extra retry handlers

### Defaults
- client supports cookie
- read timeout is 60 seconds
- Default user agent interceptor
- Dynamc base URL handler
- Azure Jackson mapper adapter
- Default retry handler with expotential strategy
- Default endpoint `AzureEnvironment.AZURE.getResourceManagerEndpoint()`

### Changes required in AutoRest
- `mapperAdapter()` to `serializerAdapter()`
