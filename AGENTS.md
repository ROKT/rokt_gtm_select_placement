# rokt_gtm_select_placement

## Project Overview

This is a public repository containing the Google Tag Manager (GTM) community
template for "mParticle by Rokt - Events". It enables partners to configure and
load the mParticle by Rokt SDK via Google Tag Manager, supporting user identity
management, event logging, and Rokt placement rendering on partner websites.

Resident expert: Alex Sapountzis (alex.sapountzis@rokt.com).

## Architecture

The repo contains a single GTM `.tpl` (template) file that defines:

1. **Template Parameters** — UI configuration groups for Identity, Log Event,
   Select Placements, and Attributes sections in the GTM console.
2. **Sandboxed JavaScript** — Builds configuration objects from tag parameters
   and injects the Rokt events wrapper script
   (`https://apps.rokt.com/store/js/gtm_wrapper_events.min.js`).
3. **Web Permissions** — Declares required GTM permissions: console logging,
   global variable access (`eventConfig`), and script injection from `*.rokt.com`.
4. **Tests** — Inline test scenarios validating script injection, window config
   writing, identity config, placement config, and failure handling.

```
template.tpl
├── ___INFO___              Tag metadata (name, brand, description)
├── ___TEMPLATE_PARAMETERS___  UI parameter definitions (JSON)
├── ___SANDBOXED_JS___      Runtime logic (builds eventConfig, injects script)
├── ___WEB_PERMISSIONS___   GTM permission declarations
└── ___TESTS___             Inline test scenarios
```

The template sets an `eventConfig` object on `window` and then loads the
external `gtm_wrapper_events.min.js` script which reads that config.

## Tech Stack

- **Language**: Google Tag Manager Sandboxed JavaScript
- **Template format**: GTM `.tpl` (Google Tag Manager Template)
- **License**: Apache License 2.0

## Development Guide

### Prerequisites

- Access to a [Google Tag Manager](https://tagmanager.google.com/) workspace
- Familiarity with GTM custom template development

### Quick Start

1. Download `template.tpl` from this repository.
2. In your GTM workspace, go to **Templates** > **New** > **Import**.
3. Upload the `.tpl` file.
4. Create a new tag using the imported template.
5. Configure with your API key and desired settings.
6. Set a trigger (e.g., page load).
7. Preview/debug in GTM before publishing.

### Testing

Follow the [testing guide](https://github.com/ROKT/gtm_wrapper/tree/master/docs/guides/how-to-test.md)
from the `gtm_wrapper` repo to set up a Testing Playground for template changes.

The `.tpl` file also contains inline test scenarios (under `___TESTS___`) that
run within the GTM template editor's built-in test runner.

### Deployment

Follow [Google's template update instructions](https://developers.google.com/tag-platform/tag-manager/templates/gallery#update_your_template)
to publish updates to the GTM Community Template Gallery.

Version history is tracked in `metadata.yaml` using commit SHAs and change notes.

## Project Structure

| Path | Description |
|---|---|
| `template.tpl` | GTM tag template (parameters, sandboxed JS, permissions, tests) |
| `metadata.yaml` | Template gallery metadata (homepage, docs URL, version history) |
| `README.md` | Project overview and setup instructions |
| `LICENSE` | Apache License 2.0 |
| `.gitignore` | Ignores `.DS_Store` |

## Key Configuration in template.tpl

The tag exposes four main configuration groups:

- **Identity** — Enable/disable IDSync (identify, login, logout, modify) with
  user identity types (email, customer ID, phone, social, etc.) and optional
  email hashing.
- **Log Event** — Enable/disable event logging with event name, type
  (Navigation, Location, Search, Transaction, etc.), and custom flags.
- **Select Placements** — Enable/disable Rokt placement rendering with sandbox
  mode, page identifier, and event listeners (OFFER_ENGAGEMENT,
  POSITIVE_ENGAGEMENT, PLACEMENT_CLOSED, etc.).
- **Attributes** — User attributes (name, address, demographics) and event
  attributes (payment type, confirmation ref, amount, conversion type) plus
  custom key-value attributes.

## Maintaining This Document

When making changes to this repository that affect the information documented
here (template parameters, deployment process, architecture, etc.), please
update this document to keep it accurate. This file is the primary reference
for AI coding assistants working in this codebase.
