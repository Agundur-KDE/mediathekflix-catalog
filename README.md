# Mediathekflix film catalogue

This repository distributes **signed catalogue metadata** for Mediathekflix. It contains no videos and no Android application source. The database is derived from the [MediathekView film list](https://liste.mediathekview.de/Filmliste-akt.xz); videos remain with their broadcasters. No rights to the linked programmes are granted by this repository.

## Downloads

The [latest release](https://github.com/Agundur-KDE/mediathekflix-catalog/releases/latest) provides:

- `manifest.json`: signed metadata including schema version, build time, size limits and SHA-256 digests.
- `manifest.sig`: RSA/SHA-256 signature over the exact manifest bytes.
- `catalog.db.gz`: gzip-compressed SQLite/FTS4 database, including the series index.
- `genres.json`: genre assignments with source IDs, attribution and per-source licenses; its digest is covered by the signed manifest.
- `download-counts.json`: snapshots of package download counters, not unique users or installations.

An independent private build process checks for new source data every six hours, tests and signs the database, and publishes only complete packages. The latest working release remains available if a build fails. Eight recent packages are retained.

## Trust boundary

Clients must verify the manifest using a public key pinned in their application **before** trusting any fields or downloading a package. They must then check both compressed and uncompressed sizes and hashes, reject rollback, and validate the database before replacing their existing catalogue. A key fetched from this repository is not an independent trust anchor. `catalog-public.pem` is provided only for inspection.

The signing key and publishing workflow are not in this public repository. Replacing a download here cannot produce a valid signature. Packages are catalogue data and must never be installed, extracted to arbitrary paths or executed as application code.

This is an independent project, not an official MediathekView or broadcaster service. Classifications and episode grouping are heuristic; availability and geographic restrictions depend on the original source.

## Genre sources

Genre coverage is partial. Exact, conservative matches from [TVmaze](https://www.tvmaze.com) are adapted under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/); [Wikidata](https://www.wikidata.org) assignments are CC0. Existing explicit catalogue title labels keep their original source terms. See genres.json for each assignment. These licenses cover the respective genre data, not the base catalogue, app or videos. Unmatched and ambiguous titles remain unclassified.
