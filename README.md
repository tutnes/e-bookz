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

## Note on `kindlekey.py`

The file `kindlekey.py` from the DeDRM tools project does not directly operate on the ebook package stored in this directory.

Based on inspection of that script, its purpose is to locate and decrypt Kindle for Mac/PC application key databases such as:

- `.kinf2018`
- `.kinf2011`
- `.rainier-2.1.1-kinf`
- `.kindle-info`

On macOS, it searches for those files in Kindle application support locations under the user's Library directory. It then extracts key material and writes `.k4i` key files.

That means:

- it is not a parser for `BookManifest.kfx`
- it is not a parser for `.azw8` or `.azw9.md` ebook payloads
- it is not a parser for the `.res` resource containers
- it is not useful for the `.asc` JSON metadata sidecars in this directory

At most, it is indirectly related to the DRM-protected files here because it targets separate Kindle application key files that other tooling may expect. Those key-source files are not present in this folder.

## Mirrored Package Paths Added To This Project

To preserve the package structure found under `/Users/taru/Library/Containers/com.amazon.Lassen/Data/Library/eBooks`, two book-package trees were copied into this workspace.

Added project-relative paths:

- `B07KPMJ7V9/0CA03070-2144-46D6-AA4C-333C438FE982/`
- `B0FH2MND28/D24099AF-0B91-4195-80A2-2221210CBF12/`
- `B0FH2MND28_EBOK/`

Copied relevant book-package artifacts only. Kindle application plugin bundles and other non-book directories were not copied.

### `B07KPMJ7V9/0CA03070-2144-46D6-AA4C-333C438FE982/`

Copied files:

- `BookManifest.kfx`
- `BookManifest.kfx-shm`
- `BookManifest.kfx-wal`
- `CR!DHWAV5D6XD73DB1MM1ZFY5A4N9SB.azw9.res`
- `CR!JRMYN8RV3X55Q6PT435ZQRHJ70X8.azw9.res`
- `CR!P21H6GAQ2H4N97N0VNMF8X6SJSGA.azw9.md`
- `CR!SMZCBEXT4N419BS75CJ2FH5PQYCF.azw8`
- `StartActions.data.B07KPMJ7V9.asc`
- `EndActions.data.B07KPMJ7V9.asc`
- `XRAY.entities.B07KPMJ7V9.asc`
- `amzn1.drm-voucher.v1.5b79c216-9766-45d3-a270-bd9dab81604f.voucher`

### `B0FH2MND28/D24099AF-0B91-4195-80A2-2221210CBF12/`

Copied files:

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

### `B0FH2MND28_EBOK/`

Copied from Windows Kindle content location:

- `/mnt/c/Users/taru/OneDrive - Conscia A S/Documents/My Kindle Content/B0FH2MND28_EBOK/`

Copied files:

- `B0FH2MND28_EBOK.azw`
- `B0FH2MND28_EBOK.mbpV2`
- `B0FH2MND28_EBOK.phl`
- `CR!6Z89KJ4MPD6WB5FCTJTS8MXWDEWJ.azw.md`
- `CR!71A6QPCG1S3VXCTQ80X9HQ7090KX.azw.res`
- `amzn1.drm-voucher.v1.941fb288-9b94-46e7-8274-bb96c0e1ac4d.voucher`

## `B0FH2MND28_EBOK` Extraction Outputs

Created artifacts:

- `B0FH2MND28_EBOK/extraction_report.md`
- `B0FH2MND28_EBOK/popular_highlights.csv`

Summary of extracted readable data:

- From `B0FH2MND28_EBOK.mbpV2` (JSON):
   - type: `EBOK`
   - ASIN/key: `B0FH2MND28`
   - GUID/ACR: `CR!2AHRHGTJS577F9PX8F50TAVTVSJP`
   - records: `2`
   - most recent read location: `8185`
   - furthest page read location: `8185`
- From `B0FH2MND28_EBOK.phl` (XML):
   - timestamp: `2026-05-31 02:10:43`
   - update id: `26`
   - popular highlight entries: `10`
   - `num_users` range: `6` to `9`

Book payload status:

- The `.azw`, `.azw.md`, `.azw.res`, and `.voucher` payload files expose metadata markers but remain DRM-protected content.
- No DRM bypass or decryption was attempted.

## Safe Next Steps

Potential follow-up work that stays within the current findings:

1. Enumerate approximate offsets of JPEG signatures inside the `.res` containers.
2. Produce a redacted metadata report that removes the user profile information.
3. Continue reverse-engineering the manifest and resource layout without touching protected book content.