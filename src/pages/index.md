---
title: CAI Soft binding API
description: Watermarking API for Durable Content Credentials
contributors:
  - https://github.com/crandmck 
---

<HeroSimple slots="heading, text"/>

# CAI Soft binding API

Provides a web API to retrieve C2PA manifest stores, given a soft binding value, a manifest identifier, or an asset.

C2PA specifies a mechanism for recovering a C2PA manifest for an asset, for example when the metadata containing the C2PA manifest has been stripped. This mechanism is a _soft binding_ (for example an invisible watermark or content fingerprint). The soft binding is used to look up the C2PA manifest within a Manifest Repository. The soft binding is described by the soft binding assertion.

For more information, see the [C2PA Soft Binding API technical specification](https://spec.c2pa.org/specifications/specifications/2.2/softbinding/Decoupled.html).

## API reference

[Try the API](api/index.md) using the Swagger UI. Read the endpoint descriptions and make test API calls.


