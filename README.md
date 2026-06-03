# e-bookz Analysis Notes

This directory appears to be a Kindle ebook package rather than a source-code project. The contents include a KFX manifest database, DRM-protected payload files, resource containers, and Kindle UI metadata sidecars.

## Files Present

- `BookManifest.kfx`
- `BookManifest.kfx-shm`
- `BookManifest.kfx-wal`
- `CR!0N17G05W3H1NXDBN0SFM9PKSWDR6.azw9.res`
- `CR!17Z4WKZYCS5TK3H9JT0BGYJK7MG5.azw8`
- `CR!QGXR8HX30D0Z122P96MK4B6KTK65.azw9.md`
- `CR!XQ6P8ZC7TH3TFEKY4YWVP2A55FWT.azw9.res`
- `StartActions.data.B0FH2MND28.asc`
- `EndActions.data.B0FH2MND28.asc`
- `amzn1.drm-voucher.v1.16adf9ce-2ebb-4c7a-9fe3-02acd1563fde.voucher`

## Work Performed

### 1. Classified the files

- Ran file-type inspection on the directory contents.
- Confirmed that `BookManifest.kfx` is a SQLite database.
- Confirmed that the two `.asc` files are JSON.
- Confirmed that the `.azw8`, `.azw9.md`, and `.voucher` files are binary data.

### 2. Inspected the KFX manifest database

Queried the SQLite manifest and found these tables:

- `ZKFXBOOKBUNDLEINFO`
- `ZKFXBOOKPIECE`
- `Z_PRIMARYKEY`
- `Z_METADATA`
- `Z_MODELCACHE`

Bundle id found in `ZKFXBOOKBUNDLEINFO`:

- `A:B0FH2MND28-0`

Indexed pieces found in `ZKFXBOOKPIECE`:

1. `CR!XQ6P8ZC7TH3TFEKY4YWVP2A55FWT`
   - Type: `KINDLE_MAIN_ATTACHABLE`
   - Path: `Library/eBooks/B0FH2MND28/D24099AF-0B91-4195-80A2-2221210CBF12/CR!XQ6P8ZC7TH3TFEKY4YWVP2A55FWT.azw9.res`
2. `e0f66016-5b01-433c-9b95-ea5b543b1400`
   - Type: `KINDLE_USER_ANOT`
   - No normal file path stored in this row
3. `amzn1.drm-voucher.v1.16adf9ce-2ebb-4c7a-9fe3-02acd1563fde`
   - Type: `DRM_VOUCHER`
   - Path: `Library/eBooks/B0FH2MND28/D24099AF-0B91-4195-80A2-2221210CBF12/amzn1.drm-voucher.v1.16adf9ce-2ebb-4c7a-9fe3-02acd1563fde.voucher`
4. `CR!QGXR8HX30D0Z122P96MK4B6KTK65`
   - Type: `KINDLE_MAIN_METADATA`
   - Path: `Library/eBooks/B0FH2MND28/D24099AF-0B91-4195-80A2-2221210CBF12/CR!QGXR8HX30D0Z122P96MK4B6KTK65.azw9.md`
5. `CR!0N17G05W3H1NXDBN0SFM9PKSWDR6`
   - Type: `KINDLE_MAIN_ATTACHABLE`
   - Path: `Library/eBooks/B0FH2MND28/D24099AF-0B91-4195-80A2-2221210CBF12/CR!0N17G05W3H1NXDBN0SFM9PKSWDR6.azw9.res`
6. `CR!17Z4WKZYCS5TK3H9JT0BGYJK7MG5`
   - Type: `KINDLE_MAIN_BASE`
   - Path: `Library/eBooks/B0FH2MND28/D24099AF-0B91-4195-80A2-2221210CBF12/CR!17Z4WKZYCS5TK3H9JT0BGYJK7MG5.azw8`

## Readable Metadata Extracted

The JSON sidecar files are the most readable artifacts in the directory.

### Book metadata

- ASIN: `B0FH2MND28`
- Content type: `EBOK`
- Title: `Children of Strife (Children of Time Book 4)`
- Author: `Adrian Tchaikovsky`
- Series: `Children of Time`
- Position in series: `4 of 4`
- Page count: `495`
- Estimated reading time: `9 hours and 54 minutes`
- Rating: `4.5`
- Review count: `1471`
- Popular highlights: `97 passages have been highlighted 1,806 times`

### Start-actions file observations

`StartActions.data.B0FH2MND28.asc` contains Kindle "About This Book" style metadata and widget definitions, including:

- welcome text
- reading time
- X-Ray teaser
- series information
- author bio widgets
- book description
- popular highlights
- citation-related recommendations

Layout class observed:

- `groupedLayoutWithFooter`

Top-level data keys observed:

- `authorBios`
- `authorBiosBSE`
- `authorSubscriptions`
- `bookDescription`
- `currentBook`
- `followSubscriptions`
- `grokShelfInfo`
- `popularHighlightsText`
- `readingPages`
- `readingTime`
- `seriesPosition`
- `welcomeText`

### End-actions file observations

`EndActions.data.B0FH2MND28.asc` contains post-reading UI and recommendation metadata, including:

- rating and review widgets
- sharing and recommendation widgets
- follow-the-author widgets
- next-in-series widget
- customer recommendation widgets
- editor picks widget

Layout class observed:

- `verticalList`

Top-level data keys observed:

- `authorBios`
- `authorBiosBSE`
- `authorSubscriptions`
- `currentBook`
- `customerProfile`
- `followSubscriptions`

Important note: the end-actions file includes user profile information (`customerProfile`) and should be treated as sensitive.

## Binary Payload Findings

### DRM-protected files

Header inspection showed that these files contain `ProtectedData` style DRM-wrapped content:

- `CR!17Z4WKZYCS5TK3H9JT0BGYJK7MG5.azw8`
- `CR!QGXR8HX30D0Z122P96MK4B6KTK65.azw9.md`
- `amzn1.drm-voucher.v1.16adf9ce-2ebb-4c7a-9fe3-02acd1563fde.voucher`

### Resource container findings

Both `.res` files appear to be structured KFX resource containers with a `CONT` header.

Observed container metadata strings include:

- `kfxgen.positionMaps`
- `kfxgen.textBlock`
- package version details
- payload SHA1 metadata
- content identifiers

Image-signature checks found:

- `CR!0N17G05W3H1NXDBN0SFM9PKSWDR6.azw9.res`
  - multiple JPEG signature hits (`FFD8FF`)
  - multiple `JFIF` strings
- `CR!XQ6P8ZC7TH3TFEKY4YWVP2A55FWT.azw9.res`
  - one JPEG signature hit (`FFD8FF`)
  - one `JFIF` string
  - one `Svg$` string

This strongly suggests that the resource containers include embedded image assets or image-like payloads alongside Kindle-specific container metadata.

## DRM and EPUB Conversion Note

No DRM removal or DRM-bypassing conversion was attempted.

The main book payload and metadata payload appear DRM-protected, and I did not attempt to strip DRM or convert the protected content into a DRM-free EPUB.

## Safe Next Steps

Potential follow-up work that stays within the current findings:

1. Enumerate approximate offsets of JPEG signatures inside the `.res` containers.
2. Produce a redacted metadata report that removes the user profile information.
3. Continue reverse-engineering the manifest and resource layout without touching protected book content.