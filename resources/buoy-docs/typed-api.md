---
title: "permissionkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["PermissionIdentity", "PermissionKind", "PermissionSession", "PermissionSessionState"]
dependencies: []
symbols: ["PermissionIdentity", "PermissionKind", "PermissionSession", "PermissionSessionState"]
related: ["api.md", "getting-started.md", "index.md"]
---

# permissionkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## PermissionKind

`Public Enum PermissionKind As Integer`

macOS permission diagnostics and explicit, non-repeating request sessions.

### Values

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Accessibility` | `PermissionKind` | `1` | — |
| `EventPosting` | `PermissionKind` | `2` | — |
| `InputMonitoring` | `PermissionKind` | `3` | — |

## PermissionSessionState

`Public Enum PermissionSessionState As Integer`

### Values

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Idle` | `PermissionSessionState` | `0` | — |
| `Waiting` | `PermissionSessionState` | `1` | — |
| `Granted` | `PermissionSessionState` | `2` | — |
| `Stopped` | `PermissionSessionState` | `3` | — |

## PermissionKit functions

### PermissionsSupported

`Public Function PermissionsSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### HasPermission

`Public Function HasPermission(kind As PermissionKind) As Boolean`

Read-only preflight. False does not distinguish denial from approval still pending.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `kind` | `PermissionKind` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### RequestPermission

`Public Function RequestPermission(kind As PermissionKind) As Boolean`

Explicit user action only. Grants apply to this requester, never to another app.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `kind` | `PermissionKind` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

## PermissionIdentity

`Public Class PermissionIdentity`

Identity diagnostics are not a promise that TCC will grant or preserve access.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Name` | `String` | No | No | — | — |
| `BundleIdentifier` | `String` | No | No | — | — |
| `ExecutablePath` | `String` | No | No | — | — |
| `ApplicationPath` | `String` | No | No | — | — |
| `IsApplicationBundle` | `Boolean` | No | No | `False` | — |
| `IsTemporary` | `Boolean` | No | No | `False` | — |
| `SigningStatus` | `Integer` | No | No | `-1` | — |
| `SigningIdentifier` | `String` | No | No | — | — |
| `TeamIdentifier` | `String` | No | No | — | — |
| `DesignatedRequirement` | `String` | No | No | — | — |
| `IsAdHoc` | `Boolean` | No | No | `False` | — |
| `HasSigningCertificate` | `Boolean` | No | No | `False` | — |

### Constructor

`Public Sub Constructor()`

No parameters.

Returns: no value.

### Summary

`Public Function Summary() As String`

No parameters.

#### Returns

| Type |
| --- |
| `String` |

## PermissionSession

`Public Class PermissionSession`

Start requests once; Refresh only preflights. No timeout, repeated prompts or auto-grant.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Kind` | `PermissionKind` | Yes | No | — | — |
| `State` | `PermissionSessionState` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(kind As PermissionKind)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `kind` | `PermissionKind` | `ByVal` | Required |

Returns: no value.

### Start

`Public Sub Start()`

No parameters.

Returns: no value.

### Refresh

`Public Sub Refresh()`

No parameters.

Returns: no value.

### StopWaiting

`Public Sub StopWaiting()`

No parameters.

Returns: no value.
