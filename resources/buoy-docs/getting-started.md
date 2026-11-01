---
title: "PermissionKit getting started"
summary: "Install and use PermissionKit with explicit configuration and resource ownership."
category: "Guides"
order: 10
keywords: ["permissions", "macos", "accessibility", "tcc", "identity"]
related: ["index.md", "api.md", "typed-api.md"]
---

# PermissionKit getting started

Install the permissionkit archive in packages. The following example checks support before reading permission state. It never requests a grant and can run as a console preflight; a requesting UI must instead be a stable installed application bundle.

```buoy
Import permissionkit

Sub Main()
    If PermissionsSupported() Then
        Dim identity As New PermissionIdentity()
        Print identity.Summary()
        If HasPermission(PermissionKind.Accessibility) Then
            Print "Accessibility is granted"
        Else
            Print "Accessibility is not currently granted"
        End If
    Else
        Print "Permission diagnostics require macOS"
    End If
End Sub
```

## Request from a button

In an installed GUI app, create a PermissionSession for the relevant PermissionKind. Call Start only after an explicit request action, then call Refresh from a timer while keeping the event loop running. Observe State rather than assuming the request call grants access immediately.

Sessions move between Idle, Waiting, Granted, and Stopped. There is no automatic timeout or permission grant. StopWaiting affects only a waiting session and cannot dismiss an OS dialog. A grant belongs to the requesting process identity; it does not authorize another app or a temporary test harness.

## Diagnose rebuilds

Construct PermissionIdentity to inspect bundle and signing fields. Compare DesignatedRequirement and signing identity when diagnosing changed permissions across builds. A matching BundleIdentifier alone does not guarantee retained access.

## Read next

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
