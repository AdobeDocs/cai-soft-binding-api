---
title: CAI Soft binding API
description: Watermarking API for Durable Content Credentials
contributors:
  - https://github.com/crandmck 
---

<HeroSimple slots="heading, text"/>

# CAI Soft binding API

Provides a web API to retrieve C2PA manifest stores, given a soft binding value, a manifest identifier, or an asset.

A  _soft binding_ in a C2PA manifest enables recovering the manifest for an asset even when the manifest has been stripped from the asset.  You can use the soft binding to look up the C2PA manifest within an online manifest repository. 

Soft bindings are described using _soft binding assertions_ such as a fingerprint computed from the digital content or an invisible watermark embedded within the digital content. These soft bindings enable digital content to be matched even if the underlying bits differ.

For more information, see:
- [Content Credentials technical specification](https://spec.c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html#_soft_bindings).
- [C2PA Soft Binding API technical specification](https://spec.c2pa.org/specifications/specifications/2.2/softbinding/Decoupled.html).

## API reference

[Try the API](api/index.md) using the Swagger UI. Read the endpoint descriptions and make test API calls.


