---
title: CAI Soft binding resolution API
description: Watermark resolution API for Durable Content Credentials
contributors:
  - https://github.com/crandmck 
---

<HeroSimple slots="heading, text"/>

# CAI Soft binding API

Provides a web API to retrieve C2PA manifest stores, given a soft binding value, a manifest identifier, or an asset.

A  _soft binding_ in a C2PA manifest enables recovering the manifest for an asset even when the manifest has been stripped from the asset.  You can use the soft binding to look up the C2PA manifest within an online manifest repository. Soft bindings are described using _soft binding assertions_ such as a fingerprint computed from the digital content or an invisible watermark embedded within the digital content. These soft bindings enable digital content to be matched even if the underlying bits differ.

For more information, see:
- [Content Credentials technical specification](https://spec.c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html#_soft_bindings).
- [C2PA Soft Binding API technical specification](https://spec.c2pa.org/specifications/specifications/2.2/softbinding/Decoupled.html).

## Workflow

Using an image with a TrustMark watermark, retrieve the watermark ID using the TrustMark `decode()` method, for example:

```py
from trustmark import TrustMark
from PIL import Image
import base64

EXAMPLE_FILE = 'path_to_watermarked_image.jpeg' 

MODE='P'
tm=TrustMark(verbose=True, model_type=MODE, encoding_type=TrustMark.Encoding.BCH_4)
stego = Image.open(EXAMPLE_FILE).convert('RGB')

wm_secret, wm_present, wm_schema = tm.decode(stego, MODE='binary')

modified_wm_secret = "2*" + wm_secret
encoded_bytes = base64.b64encode( modified_wm_secret.encode('utf-8') )
encoded_watermark_string = encoded_bytes.decode('utf-8')

print(f"Watermark: {wm_secret}")
print(f"Base64 encoded watermark: {encoded_watermark_string}")
```

Then use the `/matches/byContent` route with the the value of `encoded_watermark_string` (the  base64-encoded watermark with "2*" prepended), to fetch the manifest IDs that match the watermark.   

The API supports the following (query) parameters:
- `alg`: The fingerprint algorithm applied; must be one of the [C2PA approved fingerprint algorithms](https://opensource.contentauthenticity.org/docs/durable-cr/sb-algs). Adobe Content Authenticity uses `com.adobe.icn.dense`, the [Adobe Image Comparator Network Dense Fingerprint](https://openaccess.thecvf.com/content/CVPR2021W/WMF/html/Black_Deep_Image_Comparator_Learning_To_Visualize_Editorial_Change_CVPRW_2021_paper.html).
- `hintAlg`: The watermark algorithm applied; must be one of the [C2PA approved watermark algorithms](https://opensource.contentauthenticity.org/docs/durable-cr/sb-algs). Adobe Content Authenticity uses `com.adobe.trustmark.P`, [TrustMark Variant P](https://opensource.contentauthenticity.org/docs/durable-cr/trustmark-intro#variants).
- `hintValue`: The base64-encoded watermark with "2*" prepended. This is the value of `encoded_watermark_string` in the code above.

For example:

```sh
curl -X POST \
-T lobos-Cr.jpeg \
-H 'content-type: image/jpeg' \
-H 'x-api-key: <<API_KEY>>' \
'https://cai-msb.adobe.io/sbapi/matches/byContent?alg=com.adobe.icn.dense&hintAlg=com.adobe.trustmark.P&hintValue=MioxMDAxMDAxMTAxMTAwMDAxMDAxMTEwMDEwMDExMTAxMDAwMTExMTEwMDEwMTAwMTExMDEwMDAwMTEwMDEwMTEwMTExMA=='
```

The response will look something like this:
```json
{ "matches": 
  [
    { "manifestId":"urn-c2pa-93470c24-11e8-4879-9492-28e8625cf357-adobe",
    "endpoint":"https://cai-manifests.adobe.com/",
    "similarityScore":null }
  ]
}
```

The value of the `manifestId` property is the manifest ID.  You can use this value with the `manifests/{manifestID}` route to get the actual CBOR manifest.  For example:

<https://cai-manifests.adobe.com/manifests/urn-c2pa-93470c24-11e8-4879-9492-28e8625cf357-adobe>

You can also view the image on the Adobe Content Authenticity website, providing the manifest ID in the URL like this:

```
https://contentauthenticity.adobe.com/inspect?source=https%3A%2F%2Fcai-manifests.adobe.com%2Fmanifests%2F<<MANIFEST_ID>>
```

For example:

<https://contentauthenticity.adobe.com/inspect?source=https%3A%2F%2Fcai-manifests.adobe.com%2Fmanifests%2Furn-c2pa-93470c24-11e8-4879-9492-28e8625cf357-adobe>

## API reference

[Try the API](api/index.md) using the Swagger UI. Read the endpoint descriptions and make test API calls.


