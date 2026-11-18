# Working on assam-maps

Assam map portal and GIS data. Part of AxomRank: see README.md for the overview and roadmap.

## Layout

- `assam/`, `collection/`, `naduar/`: the web map viewers
- `data/raw/<theme>/`: byte-for-byte original KML and KMZ files
- `data/derived/<theme>/`: generated KML, GeoJSON and CSV
- `data/admin-layers/`: administrative GeoJSON layers (see `LAYERS.md`)
- `catalog/`: dataset metadata and the source registry

## Commands

- `python3 scripts/build_catalog.py && python3 scripts/validate_catalog.py`
- `python3 -m unittest discover -s tests -v`

## Rules

- Never modify `data/raw/`
- Do not present the 33-district file as today's district list
- Keep the source date and identifier for every layer
- CI fails if `catalog/` or `data/derived/` is stale, so rebuild before committing
- Commit as the `axomrank` account, in small reviewable commits.
