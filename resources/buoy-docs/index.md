---
title: "PermissionKit"
summary: "Inspect requester identity and manage explicit macOS permission request sessions."
category: "Overview"
order: 0
keywords: ["permissions", "macos", "accessibility", "tcc", "identity"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# PermissionKit

PermissionKit provides macOS permission diagnostics for the calling process: Accessibility, event posting, and Input Monitoring. It never grants access to another app, posts input events, resets TCC, or persists a cached authorization decision.

## Explicit user action

PermissionsSupported reports platform support. HasPermission is a nonprompting preflight; False does not distinguish an initial request from pending approval or denial. RequestPermission is an explicit main-UI-thread action and rejects bare executables, temporary bundles, and missing bundle IDs.

PermissionSession construction is inert. Start requests at most once per session; Refresh only preflights. Keep the application event loop alive and refresh from the UI while waiting. StopWaiting stops observation, not the system dialog.

## Identity and platforms

PermissionIdentity is diagnostic information, not proof of authorization. Keep a stable bundle ID, installed path, and signing certificate. Ad-hoc rebuilds can change the designated requirement even when the ID remains the same. Non-macOS native operations throw UnsupportedOperationException.

## Read next

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
