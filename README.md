# Idea & Usage

IPFN idea described with basic usage.

## Intro

Before reading about implementation details, please see [self-describing encoding](https://multiformats.io/),
in particular [multiaddr](https://multiformats.io/multiaddr/) and [cid](#content-id--cid).

Related: [IPLD](https://docs.ipld.io/), [IPFS](https://ipfs.io/).

### Content ID – CID

Multiformats CID eq. `bafybeigdyrzt5sfp7udm7hu76uh7y26nf3efuylqabf3oclgtqy55fbzdi` contains following data:

* [multibase](https://multiformats.io/multibase/) code: `b` name: `base32`
* [multicodec](https://multiformats.io/multicodec/) code: `0x70` name: `dag-pb`
* [multihash](https://multiformats.io/multihash/) code: `18` name: `sha2-256` bits: `256`

## Usage

### Call

Calls to IPFN happen through [multiaddr](https://multiformats.io/multiaddr/).

We can call our function on a remote node eq.

```
/dns4/ipfn.instance.remote/tcp/7111/ipfn/zFunc…54oA/tcp/8080/http/foo/bar
```

Or on local node:

```
/ipfn/zFunc…54oA/tcp/8080/http/foo/bar
```

Using a HTTP [Gateway](#gateway) through browser:

```
https://zFunc…54oA.ipfn.localhost/tcp/8080/http/foo/bar
```

## Specs

The design is created with WASM execution environment in mind but not in any way limited by it.

Most software can be compiled to WASM – architecture like `amd64` that is considered secure for sandboxing.

### Function

Functions are addressed by `ipfn` protocol code and `CID` eq. `/ipfn/zFunc…54oA`.

#### Codec

Codec determines format of the function but can also be a hint on how to resolve raw data required to execute the function.

Standard codec – one of [`dag-pb`. `dag-cbor`](https://github.com/ipld/specs/blob/master/block-layer/codecs/dag-pb.md) used by IPFS.

Note: Here is 460+ well known codecs [table](https://github.com/multiformats/multicodec/blob/master/table.csv).

## Core

### Magic

Magic happens by encoding the execution environment in CID `codec` part or inside IPFS-resolved DAG.

Docker will expose TCP port. IPFN will implement `TCP` and `HTTP`.

This eliminates needs for generating new protocols for the end-user.
It takes use of existing `TCP` based protocols.

#### WASM executors

Instead of thinking about IPFN address resolving to a function, it can resolve to a `bootstrap` which spins up docker container.

#### Stateful

Stateful systems can be easily created by creating unique content ID for a function.

This content ID can be a cryptographic public key which we can use to securely communicate with it.

#### Power of content ID

Single content ID can be used to expose a single endpoint of a container for a single person by encoding this data in execution context.

## Gateway

Gateways are not a core component but are crucial in how IPFN actually becomes useful.

In simple words they provide access to insides of functions, existing either inside or outside of a function.

### Inside Gateway

GraphQL application that provides `/query` endpoint would be considered inside gateway.

Generated code that provides HTTP (or any other) interface for your Go or JavaScript functions would be considered inside gateway.

### Public Gateway

If you want to use `HTTP` or any other arbitrary maybe not even `TCP` based protocol (RF, IoT)
you can create your own public gateway that provides access to IPFN world.

#### HTTP Gateways

IPFN can be expected to be exposed as HTTP/2.0 on `/ipfn/…` path.

## Note

Focus is on V8 (Browser) and WASM — support of Docker through extension.
