# Assam Maps: district and village map portal and open GIS data for Assam

> Assam map portal and GIS data: district and village explorer, 12 catalogued KML/KMZ map sets, and GeoJSON layers for districts, villages, constituencies, railways and more.

**[Live site](https://axomrank.github.io/assam-maps/)** · [Part of AxomRank](https://github.com/axomrank)

## At a glance

- **Map portal:** search districts and villages, and browse thematic maps in the collection viewer (Leaflet)
- **12 catalogued map sets** (1,870 placemarks), each exported as KML, GeoJSON and CSV with checksums
- **Administrative layers** in [`data/admin-layers/`](data/admin-layers/LAYERS.md): state boundary, 35 and 33 district sets, sub-districts, 26,000+ villages, 126 assembly and 14 parliamentary constituencies, headquarters, railways and energy plants
- **Reproducible:** standard-library Python builder, validator and unit tests, run in CI

## Quick start

```bash
python3 -m http.server 8000                # open http://localhost:8000
python3 scripts/build_catalog.py && python3 scripts/validate_catalog.py
python3 -m unittest discover -s tests -v
```

## Overview

Explore Assam districts and villages, browse thematic maps, and download reusable GIS exports. This repository combines the existing village portal with a catalog of 12 supplied KML/KMZ datasets containing **1,870 placemarks**. Counts include overlapping maps; they are not counts of unique places.

## Explore

- [District and village portal](assam/) — existing search and boundary viewer.
- [Map collection browser](collection/) — theme filtering, automatically loaded map previews, and downloads.
- [Naduar village map](naduar/) — existing local viewer.
- [Download catalog](catalog/README.md) — every supplied map and its available formats.

To use the interactive pages, serve the repository over HTTP. Opening HTML files directly can prevent data loading.

```bash
git clone https://github.com/axomrank/assam-maps.git
cd map
python3 -m http.server 8000
```

Open `http://localhost:8000/` or `http://localhost:8000/collection/`. No Node build or API key is required. Leaflet and basemap tiles require internet access; exports are usable offline in GIS software.

## Collection

| Theme | Supplied maps |
| --- | --- |
| Boundaries | Assam districts; India districts |
| Hydrology | Rivers |
| Transport | National highways; northeast railways |
| Settlements | Jamuguri villages; India cities |
| Heritage | Old temples in Assam |
| Elections | Lok Sabha constituencies, India reference |
| Travel | Jamugurihat routes; Uronto Apeswari |
| Mixed | Districts and rivers |

India and regional layers remain separate from Assam and local layers. The catalog scope is descriptive, not a geographic clip. The archive is an initial collection, not complete coverage of Assam.

## Repository layout

```text
assam/                  Existing Assam district/village application and data
naduar/                 Existing Naduar application and KML
collection/             Collection browser
catalog/                Dataset metadata, CSV index, download table, source registry
data/raw/<theme>/       Byte-for-byte originals with consistent filenames
data/derived/<theme>/   One folder per dataset: KML, GeoJSON, CSV, KMZ icon assets
scripts/                Reproducible conversion and validation
tests/                  Geometry conversion checks
docs/                   Development, formats, sourcing, and Assam collection plan
```

Existing portal datasets are retained separately and have not been replaced by the imported boundary collection. In particular, a supplied 33-feature district file must not be presented as today's authoritative district list.

## Formats

- **KMZ / original KML:** untouched source files; KMZ retains Google Earth styles and assets.
- **KML:** readable source XML with extracted icon assets alongside it.
- **GeoJSON:** one feature per placemark, longitude/latitude in WGS 84, with polygons, holes, lines, points, and mixed geometry collections. Names, descriptions, folders, styles, and attributes are retained as properties. Google Earth styling is not reproduced in GeoJSON.
- **CSV:** a feature table with properties and full GeoJSON geometry columns; polygons are not reduced to invented centroid points.

[Format details and optional GeoPackage/Shapefile workflows](docs/FORMATS.md).

## Rebuild and validate

Python 3.10 or later, standard library only:

```bash
python3 scripts/build_catalog.py
python3 scripts/validate_catalog.py
python3 -m unittest discover -s tests -v
```

The builder extracts KML/KMZ and regenerates exports, checksums, counts, and download links from `catalog/datasets.json`. CI checks conversions and detects stale generated files. Validation checks structure and coordinates; it does not prove polygon topology, positional accuracy, or legal boundary correctness.

## Develop and expand

Start with [development instructions](docs/DEVELOPMENT.md), follow [the contribution process](CONTRIBUTING.md), and use [the Assam collection plan](docs/COLLECTION_PLAN.md) to prioritize new themes. [The source registry](catalog/sources.csv) records researched discovery links, access notes, and collection status. Source discovery links are not downloaded datasets.

Priorities: verify provenance and dates of this collection, reconcile dated administrative boundaries, add rivers and wetlands, transport and amenities, flood/environment layers, then cultural, economic, historical, and demographic maps. Preserve source dates and identifiers so older maps remain useful without being confused with current geography.

## Provenance and reuse

The supplied files have no verified source URLs, data dates, or licenses. Their catalog status is **unverified**, and no new license is assigned to their contents. Repository availability does not establish reuse rights. Check each provider's terms before redistributing new downloads. Store a copy or reference to the applicable terms and required attribution per dataset.

Descriptions are retained as source text. The collection viewer displays plain text rather than executing embedded HTML. Combined maps can duplicate features in individual maps. Boundaries and constituency data may predate later administrative or electoral changes.

## Roadmap: future improvements

- [ ] Bring the `data/admin-layers/` files into the catalog (`catalog/datasets.json`), with source and date
- [ ] Reconcile the 33- and 35-district boundaries, and record the date and authority of each
- [ ] Add rivers and wetlands, flood layers, schools and health facilities
- [ ] Add printable district maps for exam aspirants (district headquarters, rivers, national parks)
- [ ] Add a data license (for example ODbL or CC BY 4.0) once the provenance of each layer is confirmed

## For AI agents and contributors

Read [AGENTS.md](AGENTS.md) and `docs/DEVELOPMENT.md`. Never edit `data/raw/` (byte-for-byte originals). Regenerate `data/derived/` with the builder.

Commit as the `axomrank` account. Keep changes small and reviewable, and run the repository's checks before pushing.

## Part of AxomRank

[AxomRank](https://axomrank.pages.dev) offers free, bilingual preparation for Assam government exams. Related repositories:

- **Learn:** [AxomRank app](https://axomrank.pages.dev) (the learning app; private code), [axomrank.github.io](https://github.com/axomrank/axomrank.github.io) (the home page), [floor-test-simulator](https://github.com/axomrank/floor-test-simulator) (parliamentary majority simulator)
- **Explore Assam history:** [ahom-kingdom-history](https://github.com/axomrank/ahom-kingdom-history) (illustrated Ahom kingdom website and 41 reign lessons), [assam-history-map](https://github.com/axomrank/assam-history-map) (year-by-year historical map), [assam-history-characters](https://github.com/axomrank/assam-history-characters) (character sheets for Assam's history), [assam-visual-archive](https://github.com/axomrank/assam-visual-archive) (gallery of Assam scenes and photographs), [assam-heritage-ai-art](https://github.com/axomrank/assam-heritage-ai-art) (AI art gallery of Assamese heritage)
- **Open data:** [assam-exam-pyq](https://github.com/axomrank/assam-exam-pyq) (2,398 previous-year questions with answers), [assam-exam-syllabus](https://github.com/axomrank/assam-exam-syllabus) (syllabi for 12 recruitment boards), [assam-history-sources](https://github.com/axomrank/assam-history-sources) (Kamarupa inscriptions and primary sources)
- **Publishing and brand:** [axomrank-blog](https://github.com/axomrank/axomrank-blog) (exam guides built from real papers), [assam-history-books](https://github.com/axomrank/assam-history-books) (13-book history of Assam), [axomrank-brand-assets](https://github.com/axomrank/axomrank-brand-assets) (brand kit and social media library)

## License and contact

No license file yet. Third-party layers keep their source terms. See the provenance section above.

Corrections and questions: open an issue in this repository. AxomRank is run by Angsuman Das (sole proprietor).
