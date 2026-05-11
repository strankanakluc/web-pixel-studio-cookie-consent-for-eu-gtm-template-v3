# Web Pixel Studio Cookie Consent for EU v3

A lightweight **Google Tag Manager (GTM) Consent Mode v3 template** for managing user consent in compliance with GDPR, EDPB guidelines, and other EU regulations.

> **This version (v3)** extends the standard Consent Mode v2 by activating the `developer_id.dZTNiMT` signal, which identifies the template as a verified CMP implementation to Google.

## What's New Compared to v2

| Feature | v2 | v3 |
|---------|----|----|
| Google Consent Mode 2.0 (7 types) | ✅ | ✅ |
| `ads_data_redaction` + `url_passthrough` | ✅ | ✅ |
| `developer_id.dZTNiMT` signal | ❌ | ✅ |
| Cookie-based consent (ccwps_consent) | ✅ | ✅ |

## Features

✅ **Google Consent Mode v3** – activates the `developer_id.dZTNiMT` signal
✅ **EU GDPR Compliant** – designed with GDPR and EDPB requirements in mind
✅ **7 Consent Types** – support for all Google consent types:
   - `ad_storage` – advertising cookies
   - `ad_user_data` – user data for online advertising
   - `ad_personalization` – personalized advertising
   - `analytics_storage` – analytics and performance cookies
   - `functionality_storage` – website functionality cookies
   - `personalization_storage` – personalization cookies
   - `security_storage` – security and authentication cookies

✅ **Automatically configures**:
   - `ads_data_redaction: true` – redacts ad click identifiers when `ad_storage` is denied
   - `url_passthrough: true` – preserves gclid/dclid in URLs when `ad_storage` is denied
   - `developer_id.dZTNiMT: true` – verified CMP implementation identifier

## Installation

### Step 1: Import the Template into GTM

1. Open your **Google Tag Manager** container
2. Go to **Templates** → **Tag Templates**
3. Click **New** → three dots (⋮) → **Import**
4. Upload the file `web-pixel-studio-cookie-consent-eu-v3.tpl`
5. Save

### Step 2: Create a Tag

1. Go to **Tags** → **New**
2. Select **Web Pixel Studio Cookie Consent for EU v3** as the tag type
3. Set `wait_for_update` (default: 500 ms)

### Step 3: Set Up the Trigger

- **Recommended trigger**: "Consent Initialization – All Pages"
- Ensures consent is initialized before other tags fire

### Step 4: Test and Publish

1. Test the tag in **Preview Mode**
2. Publish the container

## How It Works

The template runs BEFORE other tags (Consent Initialization phase):

1. **Sets default state** – calls `setDefaultConsentState()` with all types set to `denied` (except `security_storage` → `granted`)
2. **Sets v3 signals** – `ads_data_redaction`, `url_passthrough`, `developer_id.dZTNiMT`
3. **Reads the cookie** – if the `ccwps_consent` cookie exists, immediately updates state via `updateConsentState()`
4. When the visitor interacts with the banner, the plugin calls `gtag('consent','update',…)` and GTM responds immediately

## Category Mapping

| Cookie field  | GTM Consent signal                                   |
|---------------|------------------------------------------------------|
| `analytics`   | `analytics_storage`                                  |
| `targeting`   | `ad_storage`, `ad_user_data`, `ad_personalization`   |
| `preferences` | `functionality_storage`, `personalization_storage`   |
| *(always)*    | `security_storage` → `granted`                       |

## Recommended GA4 Tag Setup

In the Google Analytics: GA4 Configuration tag:
- Advanced Settings → Consent Settings
- Check: **Require additional consent to fire this tag**
- Consent type: `analytics_storage`

## Compatibility

This template is designed for the **Web Pixel Studio Cookie Consent for EU** WordPress plugin. The `ccwps_consent` cookie is set automatically by the plugin.

## License

[LICENSE](LICENSE)