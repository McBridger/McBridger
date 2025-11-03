# McBridger Project Versioning Strategy

This document outlines the versioning strategy for the McBridger organization's projects, which comprise multiple independent application repositories (e.g., `mac` and `mobile`). The core principle is to maintain independent versioning for each application while providing a unified release mechanism in the main `McBridger` repository.

## Core Principles

1.  **Independent Component Versioning:**
    *   Each application project within the organization (e.g., `mac` and `mobile`) will maintain its own independent version number, adhering to [Semantic Versioning (SemVer)](https://semver.org/).
    *   Changes to one application (e.g., a bug fix in the `mobile` app) will only increment its specific version number, without affecting the version of other applications.
    *   **SemVer Format:** `MAJOR.MINOR.PATCH`
        *   **MAJOR:** Incompatible API changes.
        *   **MINOR:** Add functionality in a backward-compatible manner.
        *   **PATCH:** Backward-compatible bug fixes.
    *   **Version Storage:**
        *   **macOS App (`mac/`):** Version information will be managed within the Xcode project (e.g., `Marketing Version` and `Current Project Version` in `Info.plist` or project settings).
        *   **Mobile App (`mobile/`):** Version information will be managed in `package.json` and `app.json` (or `app.config.ts`).

2.  **"Dumb" Main Repository (`McBridger/`):**
    *   The main `McBridger` repository itself does **not** have a semantic version number (e.g., `v1.0.0`). Instead, it acts as a "release aggregator" or "umbrella release" repository.
    *   Its primary role is to orchestrate and bundle specific, already-versioned artifacts from its component applications into a single, cohesive release.
    *   It does not perform builds of the child applications directly. Instead, it fetches pre-built and pre-tested artifacts.

3.  **Unified Release Mechanism:**
    *   Releases are created in the main `McBridger` repository.
    *   Each release in `McBridger` will be identified by a unique tag, typically based on a date or a descriptive name (e.g., `release-2025-11-03`, `autumn-update-2025`). This tag is **not** a semantic version for the entire product, but rather an identifier for a specific bundle of component versions.
    *   The release description will explicitly state the versions of each included component application.
    *   The release will include the compiled binary artifacts (e.g., `.app`, `.dmg`, `.apk`, `.ipa`) for all applications specified in that release.

## Workflow for Creating a Unified Release

1.  **Component Development & Versioning:**
    *   Developers work on individual applications (`mac/`, `mobile/`).
    *   Upon completion of features or bug fixes, the respective application's version is incremented according to SemVer.
    *   A Git tag corresponding to the new version (e.g., `mac-v1.2.2`, `mobile-v1.8.2`) is created in the child repository.

2.  **Component Repository CI/CD (Build & Draft Release):**
    *   A GitHub Actions workflow in each component repository (e.g., `mac`, `mobile`) is triggered by the creation of a new version tag.
    *   This workflow builds the application, runs all tests, and, if successful, creates a **draft release** in its own repository.
    *   The compiled binary artifact(s) are attached to this draft release.

3.  **Main Repository CI/CD (Unified Release Orchestration):**
    *   A GitHub Actions workflow in the `McBridger` repository (e.g., `create-unified-release.yml`) is manually triggered.
    *   The user provides inputs to this workflow:
        *   A tag for the main `McBridger` release (e.g., `release-2025-11-03`).
        *   A name for the main `McBridger` release (e.g., "November 3rd Update").
        *   The specific Git tags (versions) of the `mac` and `mobile` applications to include (e.g., `mac-v1.2.2`, `mobile-v1.8.2`).
    *   This workflow uses GitHub API calls (or dedicated actions) to:
        *   Locate the specified draft releases in the component repositories.
        *   Download the pre-built binary artifacts from these draft releases.
        *   Create a **final, public release** in the `McBridger` repository.
        *   The release description will clearly list the versions of the included `mac` and `mobile` applications.
        *   The downloaded artifacts are attached to this unified release.

## Benefits

*   **Flexibility:** Allows independent release cycles for each application. A bug fix in one doesn't force a version bump or release for the other.
*   **Clarity:** Each application's version accurately reflects its own state and changes.
*   **Efficiency:** The main repository only orchestrates, avoiding redundant builds and ensuring that released artifacts are identical to those that passed component-level tests.
*   **Traceability:** Easy to see which specific versions of each component are bundled together in a given unified release.
