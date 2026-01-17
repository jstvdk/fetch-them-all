# Purpose

Global purpose of the software is to create a dossier of an astronomical object. First iteration should focus on simpler deliverables, mainly providing proof of concept for the idea. For this we will focus on the particular object type, e.g. Supernovae remnants, and on particular output - e.g. only raw tables, images, physical quantities, literature list. Each of the stages should provide traceability of its creation process.

Later versions would include LLM post-processing, generated explanations, providing complex hypothesis and contradiction analysis.

Core idea is to simplify first days/weeks of the scientific research, providing more time for hypothesis generation, ideas iteration and speeding up the overal end-to-end scientific product build.

As a black-box, the pipeline is:

```
object ID -> Dossier
```

Inside the pipeline, we will handle name resolution, naming conflicts, accessing databases, downloading/streaming resources, building images and tables, saving results in the pre-defined uniform format, complete provenance of the workflow.

# Inputs

- Object identifier (commonly addopted use name, understandable via __SIMBAD__)
- Config file, which defines:
    - What multi-messenger bands to include
    - Additional special flags

# Outputs

- Folder with output data (images, tables);
- `index.json` with machine readable output to keep the pipeline reproducible and prone to specific re-runs;
- provenance log;
- Scientific human-readable report (markdown, pdf, html)

# Scope

## v0.1

- Name resolution
- SIMBAD query
- Radio, IR, optical, x-ray (soft,hard), gamma count map / image / built
- Raw spectra data downloaded (.fits)
- Light curves data downloaded (.fits)
- Spectra and light curves image built
- Descriptive provenance logs
- Defined manifest and provenance schema
- Compiled literature list

- **NO** LLM integration yet

# Technical stack

- python3.12+
- astroquery
- astropy
- matplotlib
- pandas

# Qaulity attributes

- reproducibility (same inputs produce same outputs)
- provenance (each step and request can be tracked)
- graceful degradation (if any of the sub-requests fail - the pipeline continue to work)
- caching

# Definition of done

- `run --object CasA --config config_casA.toml` works on clean machine
- produces index and provenance
- CI tests
- docs show how to reproduce
- at least 2 fully working providers
