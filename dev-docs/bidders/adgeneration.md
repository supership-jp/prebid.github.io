---
layout: bidder
title: Ad Generation
description: Prebid Ad Generation Bidder Adaptor
schain_supported: true
pbjs: true
pbs: no
pbs_app_supported: no
fpd_supported: true
biddercode: adgeneration
userIds: all
media_types: native
sidebarType: 1
---


### Bid Params

{: .table .table-bordered .table-striped }
| Name | Scope    | Description | Example  | Type     |
|------|----------|-------------|----------|----------|
| `id` | required | adId        | `'1234'` | `string` |

#### First Party Data

In release 1.6.4 and later, publishers should use the `ortb2` method of setting [First Party Data](https://docs.prebid.org/features/firstPartyData.html). The following fields are supported:

* ortb2.site.content.data[]

If `ad-generation.jp` is specified for ortb2.site.content.data[].name and `546` is specified for ortb2.site.content.data[].ext.segtax, the segment array objects are processed as follows:

* segment[].id: Required. Must be a string.
* segment[].value: Optional. Must be a string.
* If only id is provided (e.g., { id: "1001" }), the id is treated as a pre-arranged classification code agreed upon with the publisher.
* If both id and value are provided (e.g., { id: "news_category", value: "Sports_Sumo" }), the value is read as the value associated with the id (key).

Example first party data that's available to all bidders and all adunits:

```javascript
pbjs.setConfig({
    ortb2: {
        site: {
            content: {
                data: [{
                    name: "ad-generation.jp",
                    ext: {
                        segtax: 546
                    },
                    segment: [
                        // Only id (required, string) is provided; treated as a classification code
                        { id: "1001" }
                        // Both id (required, string) and value (optional, string) are provided
                        { id: "news_category", value: "Sports_Sumo" },
                        { id: "local_gourmet", value: "sushi" },
                        { id: "location", value: "tokyo" },
                    ]
                }]
            }
        },
    }
});
```
