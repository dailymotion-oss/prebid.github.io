---
layout: bidder
title: Newdream
description: Prebid Newdream Bidder Adapter
biddercode: newdream
aliasCode : appnexus
media_types: video,banner,native
tcfeu_supported: true
dsa_supported: true
prebid_member: true
userIds: all (with commercial activation)
schain_supported: true
coppa_supported: true
usp_supported: true
floors_supported: true
fpd_supported: false
pbjs: true
pbs: true
gvl_id: 32
sidebarType: 1
---

### Bid Params

{: .table .table-bordered .table-striped }
| Name          | Scope    | Description | Example | Type     |
|---------------|----------|-------------|---------|----------|
| `placementId` | required |             |         | `string` |
| `randomKey`   | optional |             |         | `string` |
| `invCode`     | optional |             |         | `string` |
| `member`      | optional |             |         | `string` |

Newdream is an aliased bidder for AppNexus

### Prebid Server Note

{% include dev-docs/pbjs-adapter-required-for-pbs.md %}

#### Prebid Server Test Request

The following test parameters can be used to verify that Prebid Server is working properly with the server-side Newdream adapter. This example includes an Newdream test placement ID and sizes that would match with the test creative.

```javascript
var adUnits = [
   // Banner adUnit
   {
      code: 'banner-div',
      mediaTypes: {
        banner: {
          sizes: [[300, 250], [300,600]]
        }
      },
      bids: [{
         bidder: 'newdream',
         params: {
           placementId: 13144370
         }
       }]
   },
   // Native adUnit
   {
      code: 'native-div',
      sizes: [[1, 1]],
      mediaTypes: {
        native: {
          title: {
            required: true
          },
          body: {
            required: true
          },
          image: {
            required: true
          },
          sponsoredBy: {
            required: true
          },
          icon: {
            required: false
          }
        }
      },
      bids: [{
        bidder: 'newdream',
        params: {
          placementId: 13232354,
          allowSmallerSizes: true
        }
      }]
   },
   // Video instream adUnit
   {
      code: 'video-instream',
      sizes: [[640, 480]],
      mediaTypes: {
        video: {
          playerSize: [[640, 480]],
          context: 'instream'
        },
      },
      bids: [{
        bidder: 'newdream',
        params: {
          placementId: 13232361,
          video: {
            skippable: true,
            playback_methods: ['auto_play_sound_off']
          }
        }
      }]
   },
   // Video outstream adUnit
   {
     code: 'video-outstream',
     sizes: [[300, 250]],
     mediaTypes: {
       video: {
         playerSize: [[300, 250]],
         context: 'outstream',
         // Certain ORTB 2.5 video values can be read from the mediatypes object; below are examples of supported params.
         // To note - mediafuse supports additional values for our system that are not part of the ORTB spec.  If you want
         // to use these values, they will have to be declared in the bids[].params.video object instead using the mediafuse syntax.
         // Between the corresponding values of the mediaTypes.video and params.video objects, the properties in params.video will 
         // take precedence if declared; eg in the example below, the `skippable: true` setting will be used instead of the `skip: 0`.
         minduration: 1,
         maxduration: 60,
         skip: 0,   // 1 - true, 0 - false
         skipafter: 5,
         playbackmethod: [2], // note - we only support options 1-4 at this time
         api: [1,2,3]   // note - option 6 is not supported at this time
       }
     },
     bids: [
       {
         bidder: 'newdream',
         params: {
           placementId: 13232385,
           video: {
             skippable: true,
             playback_method: 'auto_play_sound_off'
           }
         }
       }
     ]
   },
   // Banner adUnit in a App Webview
   // Only use this for situations where prebid.js is in a webview of an App
   // See Prebid Mobile for displaying ads via an SDK
   {
     code: 'banner-div',
     mediaTypes: {
       banner: {
         sizes: [[300, 250], [300,600]]
       }
     }
     bids: [{
       bidder: 'newdream',
       params: {
         placementId: 13144370,
         app: {
           id: "B1O2W3M4AN.com.prebid.webview",
           geo: {
             lat: 40.0964439,
             lng: -75.3009142
           },
           device_id: {
             idfa: "4D12078D-3246-4DA4-AD5E-7610481E7AE", // Apple advertising identifier
             aaid: "38400000-8cf0-11bd-b23e-10b96e40000d", // Android advertising identifier
             md5udid: "5756ae9022b2ea1e47d84fead75220c8", // MD5 hash of the ANDROID_ID
             sha1udid: "4DFAA92388699AC6539885AEF1719293879985BF", // SHA1 hash of the ANDROID_ID
             windowsadid: "750c6be243f1c4b5c9912b95a5742fc5" // Windows advertising identifier
           }
         }
       }
     }]
   }
];
```
