# Eye By Proctorme Documentation Project

This repository contains the complete documentation for **Eye By Proctorme**, a lightweight, privacy-focused proctoring widget designed for modern online assessments.

## About This Documentation Project

This is a **documentation-only repository** that houses all the guides, API references, and usage instructions for the Eye By Proctorme proctoring solution. The documentation is built using MkDocs and deployed automatically via GitHub Actions.

## Documentation Structure

The documentation is organized into the following sections:

### Getting Started
- [Installation](docs/installation.md) - How to install the widget with a single script tag
- [Quick Start](docs/quick-start.md) - Complete guide to integrating and using the widget in minutes
- [Configuration](docs/configuration.md) - Detailed configuration options for the widget

### Core Features
- [API Key Management](docs/api-key.md) - How to find and manage your API key with domain restrictions
- [API Methods](docs/api-methods.md) - Available methods: `init()`, `on()`, `endProctoring()`
- [Events](docs/events.md) - Event-driven architecture and available events
- [Payload Types](docs/payload-types.md) - Structure of data returned by events

### Additional Information
- [Browser Support](docs/browser-support.md) - Supported browsers (Chrome, Firefox, Edge latest)
- [Webhooks](docs/webhooks.md) - Real-time notifications for suspicious events
- [License](docs/license.md) - Commercial licensing terms

## Building the Documentation

This documentation site is built using MkDocs. To build and serve it locally:

1. Install MkDocs and the material theme:
   ```bash
   pip install mkdocs mkdocs-material
   ```

2. Serve the documentation locally:
   ```bash
   mkdocs serve
   ```

3. Build the static site:
   ```bash
   mkdocs build
   ```

## Deployment

The documentation is automatically deployed via GitHub Actions when changes are pushed to the main branch. The workflow:
- Builds the documentation with MkDocs
- Deploys to an S3 bucket
- Invalidates CloudFront cache
- Uses configurable variables for bucket name and other settings

## Repository Structure

- `docs/` - Contains all the markdown documentation files
- `mkdocs.yml` - Configuration for the MkDocs site
- `.github/workflows/` - GitHub Actions workflow for deployment
- `requirements.txt` - Python dependencies for building the documentation
- `site/` - Built documentation site (excluded from git by .gitignore)

## License

The documentation in this repository is provided as part of the Eye By Proctorme commercial software documentation. For information about the software licensing, see the [License documentation](docs/license.md).

## Support

For documentation issues or suggestions, please contact the Eye By Proctorme team.
