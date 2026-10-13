# Publishing releases

This repository hosts public Windows downloads and user documentation for multiple apps. Keep application source code, build logs, local settings, credentials, and debugging screenshots out of this repository. Upload binaries as GitHub Release assets, not Git commits.

## Product tags and download links

- EasyClick releases use `easyclick-vX.Y.Z` tags.
- Existing EasyKeepFocus `v1.x` tags remain unchanged for compatibility. Use `easykeepfocus-vX.Y.Z` for future EasyKeepFocus releases.
- Create product releases with `--latest=false`. GitHub has one repository-wide latest release, not a separate latest release for each product. The existing latest release remains EasyKeepFocus `v1.4.2` so older download links keep working.
- Update the product's row in the root README and its user guide to point to the new explicit product tag after publishing.
- Keep the former repository names `easykeepfocus-releases` and `focuskeeper-releases` unused so GitHub can continue redirecting old URLs.

## Assets and release notes

For EasyClick, upload only `EasyClick.exe`, `EasyClick-X.Y.Z-win-x64.zip`, and `SHA256SUMS.txt`. For EasyKeepFocus, upload its versioned portable ZIP and include its SHA-256 digest in the release notes.

Release notes and user documentation are written in English. Verify each file's size and SHA-256 digest before publishing. Keep released assets immutable: a changed binary belongs in a new version, not an overwrite of an existing release.

Application builds remain in their private source repositories. A source repository's default `GITHUB_TOKEN` cannot publish to this repository. Automated publishing requires a dedicated token with Contents write access to this repository, stored as a secret in the relevant source repository. EasyClick uses `PUBLIC_RELEASE_TOKEN` and the optional `PUBLIC_RELEASE_REPOSITORY` variable; its local publishing script can instead use an authenticated GitHub CLI session.
