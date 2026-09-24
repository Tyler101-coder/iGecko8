# iGecko8

Cross-platform mobile configuration profiles for **iOS** and **Android Enterprise**.

iGecko8 provides a baseline of extreme security, performance tuning, and jailbreak/root resistance for managed devices.

> **Created by:** LifeStudio MDM Services Inc  
> **Security level:** Extreme  
> **Supported platforms:** iOS / iPadOS (Apple `.mobileconfig`), Android Enterprise (Android Management API JSON)

---

## ⚠️ Disclaimer

- LifeStudio MDM Services Inc is a **fictional organisation** used for demonstration purposes.
- The included root certificate, passwords, domains, and endpoints are **placeholders**.
- Do **not** deploy this in production without replacing every placeholder and reviewing the policy against your own security requirements.
- This project is not affiliated with Apple Inc. or Google LLC.

---

## 📦 Contents

| File | Platform | Format | How it is applied |
|------|----------|--------|-------------------|
| `iGecko8.mobileconfig` | iOS / iPadOS | Apple Configuration Profile (plist XML) | User install via Safari, email, AirDrop, or MDM |
| `iGecko8-policy.json` | Android Enterprise | Android Management API Policy (JSON) | Pushed by an EMM/MDM console or a Device Policy Controller (DPC) app |

---

## 🚀 Installation

### iOS / iPadOS

1. Transfer `iGecko8.mobileconfig` to the device (AirDrop, email attachment, Safari download, or MDM).
2. Open **Settings → Profile Downloaded**.
3. Tap **Install**, enter the device passcode, and agree to the consent text.
4. The device will restart to apply all system-level changes.

> The profile is locked with a removal password. Change it before deployment.

### Android Enterprise

Android does **not** support user-installable `.mobileconfig` files. The JSON policy must be applied through one of:

- **Android Management API** – call `enterprises.policies.patch` with the JSON body.
- **EMM / MDM console** – import the JSON as a policy template (Intune, Workspace ONE, etc.).
- **Custom DPC app** – read the JSON and enforce it via `DevicePolicyManager`.

> Tapping the JSON file on an Android device will not install anything.

---

## 🔧 Customisation checklist

Before using these files, replace the following:

- [ ] `lifestudio.example` → your real domain
- [ ] Root CA certificate payload → your real root certificate
- [ ] VPN, DNS, Wi-Fi, and mail server endpoints
- [ ] `RemovalPassword` in the iOS profile
- [ ] Android package names in `applications` and `vpnConfig`
- [ ] `alwaysOnVpnPackage` and `com.lifestudio.mdm.shield` references

---

## 🛡️ Security notes

- The iOS root certificate is a **base64 placeholder** and will not chain to a real CA.
- The removal password is hardcoded in plaintext. Use a secret manager or MDM variable.
- Android `commonCriteriaMode` and `untrustedAppsPolicy` are strict. Test on a small device group first.
- Always validate profiles in a lab before broad deployment.

---

## 📁 Repository layout
