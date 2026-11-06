# SUMMING BUS 2+ — Official update channel

Publisher: BRUNO AUDIO  
Repository: https://github.com/luisbarria2626-lgtm/BRUNO-AUDIO-UPDATES

## Status

**Not yet active.** No downloadable updates have been released. Do not treat this repository or an HTTPS response alone as proof that an executable is authentic.

The Windows updater is a separate JUCE application launched from SUMMING BUS 2+'s SETTINGS > CHECK FOR UPDATES menu.

## Planned production endpoint

`https://raw.githubusercontent.com/luisbarria2626-lgtm/BRUNO-AUDIO-UPDATES/main/updates/summing-bus-2/latest.json`

Do **not** create or publish `latest.json` until an actual installer is released and the updater's authenticity checks are ready.

## Planned manifest fields

```json
{
  "product": "SUMMING BUS 2+",
  "version": "1.0.1",
  "installer_url": "https://github.com/luisbarria2626-lgtm/BRUNO-AUDIO-UPDATES/releases/download/v1.0.1/BRUNO-AUDIO-SUMMING-BUS-2-Setup.exe",
  "sha256": "THE_REAL_64_CHARACTER_INSTALLER_SHA256"
}
```

This is a **schema example only**, not a release. The program currently accepts the three fields `version`, `installer_url`, and `sha256` plus product name. A GitHub Release download will redirect to a GitHub asset host. The existing JUCE downloader has `withNumRedirectsToFollow(0)`, so that code must be carefully updated and tested before the channel is activated.

## Production security gate

1. Obtain a genuine code-signing certificate for the intended software publisher; never place its private key in this public repository.
2. Validate the publisher certificate with Windows Authenticode and a trusted publisher identity. Inspect actual verification implementation, including certificate-chain, revocation and signing policy.
3. Authenticate release metadata independently (for example, with a signed manifest and an embedded public verification key) to prevent attackers who modify release metadata from redirecting the updater to an unintended, even signed, package.
4. Verify the downloaded installer's SHA-256, product identity, version, signature and authorization before execution.
5. Check that an audio host is not running, get explicit user consent, and install outside the DAW. Preserve rollback support.
6. Validate normal operation and failure cases on a real Windows test environment.

### Current version

SUMMING BUS 2+ currently reports version `1.0.0` in the development setup. There is no published update yet.
