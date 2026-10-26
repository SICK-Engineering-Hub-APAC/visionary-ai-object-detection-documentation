# Visionary AI Object Detection Monitoring Documentation

Public GitHub Pages documentation for the SICK Visionary AI Object Detection
Monitoring application.

Site: https://sick-engineering-hub-apac.github.io/visionary-ai-object-detection-documentation/

## Public Routes

```text
/                                                                  Documentation landing page
/usage-manual/                                                     Latest end-user manual
/manuals/visionary-ai-object-detection-monitoring/versions.html    Version selector
/manuals/visionary-ai-object-detection-monitoring/v1.0.0/          Versioned end-user manual
```

## Repository Layout

```text
.github/workflows/deploy-pages.yml                                  Tag-triggered Pages deployment
assets/                                                             Shared landing-page assets
manuals/visionary-ai-object-detection-monitoring/manifest.json      Manual metadata and versions
manuals/visionary-ai-object-detection-monitoring/versions/v1.0.0/   Supplied HTML manual and assets
tools/Build-Site.ps1                                                Static-site builder
tools/release-docs.sh                                               Annotated release tag helper
_site/                                                              Generated output (Git ignored)
```

## Local Build

```powershell
.\tools\Build-Site.ps1
```

Open `_site/index.html` in a browser. The manual includes its HTML, styles,
scripts, icons, and screenshots for offline viewing. Each manual version also
ships its REST API contract (`api/openapi.yaml`) and the optimized settings
file (`downloads/optimized-settings_v1.0.0.json`).

The v1.0.0 manual targets application v1.0.0. The people-detection network
model is supplied separately by SICK and is not included. The application
requires the Deep Learning Classification device license (SICK part
no. 1614850). Verify network addresses, firmware, deployed settings, and
permissions before operating live equipment.

## Publish a Release

GitHub Pages must use **GitHub Actions** as its publishing source in the
repository's Settings > Pages. The workflow builds and deploys the tagged
commit when a `v*` or `manual-*` tag is pushed. It can also be run manually.

For a new manual version, add its complete HTML and assets under
`manuals/visionary-ai-object-detection-monitoring/versions/<version>/`, add the
version and compatibility information to the manifest, and update `latest`.
Keep previous version directories and manifest entries to preserve versioned
URLs.

```bash
git add .
git commit -m "Update Visionary AI Object Detection Monitoring documentation"
git push origin main
bash tools/release-docs.sh
```

The release helper builds locally, reads the default tag from the manifest's
`latest` field, refuses existing tags, and pushes an annotated tag. An explicit
tag can be supplied with `--tag v1.0.1`. Each new tag deploys the complete site;
the latest-manual route follows the manifest, not the tag name. Do not reuse or
move a published release tag.