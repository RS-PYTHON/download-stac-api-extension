# STAC API - Download Extension Specification

- [STAC API - Download Extension Specification](#stac-api---download-extension-specification)
  - [Overview](#overview)
  - [Link Relations](#link-relations)
  - [Endpoints](#endpoints)

## Overview

- **Title:** Download
- **OpenAPI specification:** [openapi.yaml](openapi.yaml)
- **Conformance Classes:**
  - <https://api.stacspec.org/v1.0.0/download>
- **Scope:** STAC API - Features
- **[Extension Maturity Classification](https://github.com/radiantearth/stac-api-spec/tree/v1.0.0/README.md#maturity-classification):** Pilot
- **Dependencies**:
  - [STAC API - Features](https://github.com/radiantearth/stac-api-spec/tree/v1.0.0/ogcapi-features)
- **Owner**: @vprivat-ads

The STAC API Download Extension adds a dedicated endpoint to download an asset: `/collections/{collectionId}/items/{itemId}/download/{assetId}`.

The purpose of this endpoint is to perform the necessary tasks (authentication, authorization, data retrieval, pre-signed URL generation)
in order to effectively download an asset data, usually from an S3 bucket that might not be publicly accessible or even known from the user.

## Link Relations

As the download links will usually be filled in the `href` field of each asset
(or if necessary using the [alternate-assets](https://github.com/stac-extensions/alternate-assets) extension),
this conformance class does not require the implementation of any new link relation.

## Endpoints

| Endpoint                                                        | Returns                  | Success Status | Description               |
| --------------------------------------------------------------- | ------------------------ | -------------- | ------------------------- |
| `/collections/{collectionId}/items/{itemId}/download/{assetId}` | application/octet-stream | 200, 307       | Returns asset binary data |

STAC APIs implementing the *STAC API - Download* conformance class must support HTTP GET operation at
`/collections/{collectionId}/items/{itemId}/download/{assetId}`, with following return codes:

- 200 if the request is successful and the server returns the binary data directly
- 307 if the request is successful and the server redirects to a temporary URI
set in the [Location](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Location) header
(for example, an S3 [presigned URL](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html))
- 404 if a resource is not found (collection, item or asset)

---

![](https://raw.githubusercontent.com/RS-PYTHON/.github/refs/heads/main/profile/banner_logo.jpg)

This project is funded by the EU and ESA.
