# Changelog

## [0.1.0] — 2026-04-29

### Added
- `import/` folder — place ARM JSON detection rules here for conversion
- `Detections/` folder — output destination for converted YAML files
- `Detections/{dev,test,flight,prod,unclassified}/` — state-based subdirectories
- `.github/workflows/convert-imports.yml` — converts ARM JSON rules from `import/` to YAML using `tentacle-conv` (downloaded from GitHub releases, SHA256-verified). Handles collisions by quarantining sources to `import/_conflicts/`, injects `state: dev` into every generated YAML, includes concurrency control and job summary
- `.github/workflows/route-detections.yml` — reads `state:` field from YAML files under `Detections/` and routes them to `dev/`, `test/`, `flight/`, `prod/`, or `unclassified/`
