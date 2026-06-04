# B0FH2MND28_EBOK Extraction Report

This report summarizes non-decryption extraction results from files in this folder.

## Source Files

- B0FH2MND28_EBOK.mbpV2
- B0FH2MND28_EBOK.phl
- B0FH2MND28_EBOK.azw
- CR!6Z89KJ4MPD6WB5FCTJTS8MXWDEWJ.azw.md
- CR!71A6QPCG1S3VXCTQ80X9HQ7090KX.azw.res
- amzn1.drm-voucher.v1.941fb288-9b94-46e7-8274-bb96c0e1ac4d.voucher

## Structured Metadata (Readable)

From B0FH2MND28_EBOK.mbpV2 (JSON):

- md5: d2c83328ba709f4f81c25430e328ec42
- payload.type: EBOK
- payload.key (ASIN): B0FH2MND28
- payload.guid: CR!2AHRHGTJS577F9PX8F50TAVTVSJP
- payload.acr: CR!2AHRHGTJS577F9PX8F50TAVTVSJP
- records count: 2
- kindle.most_recent_read location: 8185
- kindle.lpr location: 8185
- record creation time: 2026-06-02 20:52:25.0

From B0FH2MND28_EBOK.phl (XML):

- popular.timestamp: 2026-05-31 02:10:43
- popular.update_id: 26
- content.type: EBOK
- content.key (ASIN): B0FH2MND28
- content.guid: CR!2AHRHGTJS577F9PX8F50TAVTVSJP
- popular_highlight entries: 10
- num_users range: 6 to 9

## Highlight Ranges Export

All popular highlight ranges were exported to:

- popular_highlights.csv

## Binary Payload Observations

Readable marker strings are present in binary payload files, but the core book payload remains DRM-protected.

Observed marker examples:

- B0FH2MND28_EBOK.azw: ProtectedData, AES/CBC/PKCS5Padding, SHA256withRSA, amzn1.drm-voucher identifiers
- amzn1.drm-voucher...voucher: ProtectedData, CLIENT_ID, HmacSHA256, client_restrictions, ClippingLimit, TextToSpeechDisabled
- CR!71A6QPCG1S3VXCTQ80X9HQ7090KX.azw.res: kfxgen.textBlock and kfxgen metadata strings

No DRM bypass or content decryption was performed.
