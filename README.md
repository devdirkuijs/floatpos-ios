# FloatPOS — iOS shell

A thin Capacitor wrapper that turns the live FloatPOS web app into an
installable iOS app. It does **not** contain a copy of FloatPOS — the app
loads **https://floatpos.co.za** in a native WebView, so every normal FloatPOS
deploy (commit → Netlify) updates the iOS app automatically too.

- **App name:** FloatPOS
- **Bundle id:** `za.co.floatpos.app`
- **Loads:** https://floatpos.co.za
- **Capacitor:** 8.x · builds on GitHub Actions (`macos-latest`)
- **Printer:** no native plugin — MobiPrint 5 / MobiIoT is Android-only; iOS
  uses the web app’s Web Bluetooth / `window.print()` paths

Sibling Android shell: [devdirkuijs/floatpos-android](https://github.com/devdirkuijs/floatpos-android).

---

## Build

Push to `main` (or run **Actions → Build FloatPOS iOS → Run workflow**). The
workflow runs `npx cap add ios`, generates icons/splash, syncs Capacitor, and
archives an unsigned `.xcarchive` artifact for local signing / TestFlight.

Apple signing secrets are not required for the archive step. To export an IPA
for TestFlight, add certs/profiles later and extend the workflow.

---

## When do I need to rebuild the app?

- Day-to-day FloatPOS UI changes ship via Netlify. No new native build.
- Rebuild for: app name, icon/splash, the URL it loads, or native plugins
  (camera, etc.).
