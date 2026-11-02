# macOS permission prompts

Reusable macOS permission diagnostics and explicit request sessions. Import
`permissionkit` from the sealed package. It supports Accessibility, input event
posting and Input Monitoring for the **calling process**. It does not grant access
to another app, post events, reset TCC, or persist a cached permission decision.

Use a request button, keep the application event loop alive, and refresh status
while waiting. Sessions impose no timeout and never grant permission automatically.
Unsupported platform operations throw `UnsupportedOperationException`.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add permissionkit --git https://github.com/BuoyBay/permissionkit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
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

## Platform and scope

The active Accessibility/input permission sessions are macOS-specific. Diagnostic identity and request context must be preserved by the host application.

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer permissionkit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
