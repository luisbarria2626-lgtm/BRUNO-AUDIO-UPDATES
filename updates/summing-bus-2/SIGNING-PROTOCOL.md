# BRUNO AUDIO — Signed update manifest protocol (draft)

**Status:** implementation prepared, local Windows build and end-to-end verification still pending. No installable release is published.

## Release files

The updater downloads:

- `updates/summing-bus-2/latest.json`
- `updates/summing-bus-2/latest.json.sig`

The second file is an ASCII lowercase hexadecimal representation (768 characters, optional trailing LF) of an RSA-3072 / SHA-256 PKCS#1 v1.5 signature computed over the **exact bytes** of `latest.json`. Do not edit or reformat JSON after signing.

Example `latest.json` structure (NOT an actual release):

```json
{
  "product": "SUMMING BUS 2+",
  "version": "1.0.1",
  "installer_url": "https://github.com/luisbarria2626-lgtm/BRUNO-AUDIO-UPDATES/releases/download/v1.0.1/BRUNO-AUDIO-SUMMING-BUS-2-Setup.exe",
  "sha256": "REPLACE_WITH_REAL_64_CHARACTER_INSTALLER_HASH"
}
```

### Authentication

The public RSA modulus and exponent are compiled into the separate Windows JUCE updater. The private signing key must never be added to GitHub, release assets, source-control history, or a distribution installer. The developer's proposed Windows key store uses DPAPI CurrentUser encryption; operational production keys should ideally use a dedicated hardware-backed signing process with a documented recovery and rotation procedure.

Signature verification must complete before the updater trusts `version`, `installer_url` or `sha256` fields. A missing or invalid signature results in a blocked update.

### Installer security remains separate

A valid metadata signature **does not** authorize an installer to execute. The updater must continue to verify the installer SHA-256 and a trusted Windows Authenticode code-signing certificate matching its configured publisher identity. Without that identity, downloading/installing is disabled. Require explicit consent, host shutdown, and rollback testing before enabling production updates.

### Operational state

The existing version is `1.0.0`. No `latest.json`, `latest.json.sig`, or new installer has been published yet, so the correct current updater result remains **NO RELEASE PUBLISHED YET**.
