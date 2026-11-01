---
title: "PermissionKit API"
summary: "Public types, operations, error behavior, and limits for PermissionKit."
category: "Reference"
order: 20
keywords: ["permissions", "macos", "accessibility", "tcc", "identity"]
symbols: ["PermissionsSupported", "PermissionKind", "PermissionSessionState", "PermissionIdentity", "HasPermission", "RequestPermission", "PermissionSession", "PermissionSession.Refresh"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# PermissionKit API

| API | Contract |
| --- | --- |
| PermissionsSupported() | True on macOS, False elsewhere. |
| PermissionKind | Accessibility, EventPosting, InputMonitoring. |
| HasPermission(kind) | Nonprompting current-process preflight. |
| RequestPermission(kind) | Explicit main-thread request; caller identity must be a suitable installed bundle. |
| PermissionIdentity | Name, BundleIdentifier, ExecutablePath, ApplicationPath, IsApplicationBundle, IsTemporary, signing/certificate/team fields, DesignatedRequirement. |
| PermissionIdentity.Summary() | Human-readable diagnostic identity summary. |
| PermissionSession(kind) | Inert session with read-only Kind and State. |
| PermissionSession.Start() | Request at most once, preflighting existing access first. |
| PermissionSession.Refresh() | Recheck Waiting/Granted access without requesting again. |
| PermissionSession.StopWaiting() | Move Waiting to Stopped; does not cancel an OS dialog. |
| PermissionSessionState | Idle, Waiting, Granted, Stopped. |

## Failure and observation

Invalid kinds reject. Unsupported platform operations throw UnsupportedOperationException. If Start throws before a request returns, the session remains Idle and the caller may retry after correcting the failure. A preflight False is deliberately not an error code or durable denial state. Refresh can return a previously Granted session to Waiting if access is no longer present.

## Read next

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
