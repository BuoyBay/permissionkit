# PermissionKit 0.1.0

Reusable macOS permission diagnostics and explicit request sessions. Import
`permissionkit` from the sealed package. It supports Accessibility, input event
posting and Input Monitoring for the **calling process**. It does not grant access
to another app, post events, reset TCC, or persist a cached permission decision.

- `PermissionsSupported()` identifies macOS support.
- `New PermissionIdentity()` inspects the current bundle name, ID, path, signing
  identifier, team, certificate presence and designated requirement. This is a
  diagnostic snapshot, not proof of authorization.
- `HasPermission(kind)` performs a nonprompting preflight. False can mean approval
  is pending; it does not reliably distinguish denial from a first request.
- `RequestPermission(kind)` requests access explicitly on the main UI thread.
  Bare executables, temporary bundles and missing bundle IDs are rejected.
- `New PermissionSession(kind)` is inert. `Start()` requests at most once per
  session; `Refresh()` only preflights. States are Idle, Waiting, Granted and
  Stopped. A failed `Start()` that throws leaves the session Idle so the caller
  can correct the failure and retry. `StopWaiting()` stops observation; it
  cannot cancel an OS dialog.

Use a request button, keep the application event loop alive, and refresh status
while waiting. Sessions impose no timeout and never grant permission automatically.
Unsupported platform operations throw `UnsupportedOperationException`.

## Identity across builds

Keep the bundle ID and installed location consistent. An unchanged signed binary
retains its code identity. Rebuilding an ad-hoc signed binary changes its code
requirement; the same ID alone cannot promise that macOS will retain grants.
For rebuilds, use a consistent signing certificate and compare designated
requirements. Permission grants apply to the calling application identity.

See [Apple TN3127](https://developer.apple.com/documentation/technotes/tn3127-inside-code-signing-requirements)
for code-signing requirements.
