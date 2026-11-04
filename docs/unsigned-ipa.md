# Unsigned iOS IPA

The manual `Unsigned iOS IPA` workflow builds the `HermesMobile` scheme in
`Release` for `iphoneos` with code signing disabled and packages the complete
`HermesMobile.app` bundle as `HermesMobile-unsigned.ipa`.

Run it from the repository's **Actions** tab using **Unsigned iOS IPA → Run
workflow**. The workflow does not use Apple certificates, provisioning
profiles, signing credentials, App Store Connect, or TestFlight.

Before installing the artifact on a real iPhone, an external signing process
must sign the app and every embedded bundle under `Payload/HermesMobile.app`:

- `HermesShareExtension.appex`
- `HermesLiveActivityWidget.appex`
- `HermesNotificationService.appex`
- Any embedded frameworks that require signing

The signer must use provisioning profiles and entitlements compatible with the
bundle identifiers and targets. In particular, the main app and extensions
use application-group entitlements; the main app and notification service also
use keychain-access groups, and the main app uses push/time-sensitive
notification entitlements. The unsigned artifact contains entitlement
placeholders from the project but has no valid signatures, so it is not
installable until the external signer applies valid profiles and signatures.
