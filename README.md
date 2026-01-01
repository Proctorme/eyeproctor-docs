# Eye By Proctorme Documentation

**Eye By Proctorme** is a lightweight, privacy-focused proctoring widget designed for modern online assessments. It provides real-time AI-powered monitoring with minimal setup and maximum transparency.

## Overview

Eye By Proctorme is a browser-based proctoring solution that:
- Runs entirely in the browser
- Integrates via a single script tag
- Provides real-time AI-powered monitoring
- Offers face presence & multiple face detection
- Includes audio activity monitoring
- Features tab focus tracking
- Emits real-time events for integration

## Table of Contents

### Getting Started
- [Installation](docs/installation.md) - How to install the widget with a single script tag
- [Quick Start](docs/quick-start.md) - Complete guide to integrating and using the widget in minutes
- [Configuration](docs/configuration.md) - Detailed configuration options for the widget

### Core Features
- [API Key Management](docs/api-key.md) - How to find and manage your API key with domain restrictions
- [API Methods](docs/api-methods.md) - Available methods: `init()`, `on()`, `endProctorme()`
- [Events](docs/events.md) - Event-driven architecture and available events
- [Payload Types](docs/payload-types.md) - Structure of data returned by events

### Additional Information
- [Browser Support](docs/browser-support.md) - Supported browsers (Chrome, Firefox, Edge latest)
- [Webhooks](docs/webhooks.md) - Real-time notifications for suspicious events
- [License](docs/license.md) - Commercial licensing terms

## Key Capabilities

- **Face presence & multiple face detection**
- **Periodic face recognition snapshots**
- **Audio activity monitoring**
- **Tab focus tracking**
- **Event-driven integration API**

## Integration Process

1. **Install** the widget by adding a single script tag to your HTML
2. **Load** the widget using `LoadProctormeWidget()`
3. **Configure** your session with required parameters
4. **Initialize** the widget with your configuration
5. **Listen** to events for real-time monitoring
6. **End** the session when complete

## Configuration Requirements

The widget requires a configuration object with the following required fields:
- `apiKey` - Your organization's API key
- `assessmentId` - Unique identifier for the assessment
- `assessmentTitle` - Human-readable title of the assessment
- `candidateId` - Unique identifier for the candidate
- `candidateEmail` - Candidate's email address
- `candidateFirstName` and `candidateLastName` - Candidate's name
- `institutionName` - Name of the institution
- `examDuration` - Duration of the exam in seconds

## Events

The widget emits various events including:
- `STARTED` - When proctoring begins
- `END_PROCTORING` - When proctoring ends
- `FACE_ABSENCE` - When no face is detected
- `MULTIPLE_FACE` - When multiple faces are detected
- `SOUND_DETECTED` - When sound is detected
- `TAB_NOT_FOCUS` - When candidate switches tabs
- `PERIODIC_SNAPSHOT` - Periodic face snapshots

## License

Eye By Proctorme is commercial software provided under a proprietary, pay-per-use license. Access requires registration, a valid API key, and domain restrictions.

## GitHub Workflow

This repository includes a GitHub Actions workflow for deploying documentation to production:
- Triggers on pushes to the main branch
- Builds the documentation with MkDocs
- Deploys to an S3 bucket
- Invalidates CloudFront cache
- Uses configurable variables for bucket name and other settings
