# airports-247.com

The public site for Airports 24/7: a homepage, a privacy policy, and terms of
service. It exists to satisfy the App Domain requirements on the Google Cloud
OAuth consent screen (Branding page) so the project's OAuth app can be moved
from **Testing** to **In production**, which is what stops refresh tokens
expiring after seven days.

Static HTML. No build step, no generator, no JavaScript, no dependencies.

## Files

| File | Purpose |
|---|---|
| `index.html` | Homepage. Describes the project's functionality and links to both policies — Google requires both. |
| `privacy.html` | Privacy policy. Carries the YouTube API Services disclosures. |
| `terms.html` | Terms of service. Links the YouTube ToS and states users are bound by it. |
| `style.css` | The only stylesheet. |
| `CNAME` | Custom domain for GitHub Pages. Do not delete — Pages rewrites it from repo settings. |

## Before first publish

Replace the contact email placeholder in all three pages:

```
sed -i 's/CONTACT_EMAIL_PLACEHOLDER/you@example.com/g' index.html privacy.html terms.html
```

Grep for `CONTACT_EMAIL_PLACEHOLDER` afterwards to confirm none remain.

## Deploying

1. Push to a **public** repo (GitHub Pages needs public on the free tier).
2. Settings → Pages → Source: deploy from `main`, root.
3. Settings → Pages → Custom domain: `airports-247.com`. Set this **before**
   changing DNS, so the hostname cannot be claimed by someone else.
4. DNS at the registrar: four A records on `@` →
   `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`,
   and a `www` CNAME → `airports247.github.io`. Remove any pre-existing records
   the previous host left on `@`.
5. Wait for the certificate, then tick **Enforce HTTPS**.
6. Verify the domain in Google Search Console (TXT record), signed in as the
   Google account that owns the Cloud project.

## Constraints these pages are written against

Do not edit them into breach of the following without checking the sources.

- The homepage must describe the app's functionality and must not be only a
  login page; it must link the privacy policy, and that link must match the URL
  entered on the consent screen.
  <https://support.google.com/cloud/answer/15549049>
- The privacy policy must be hosted on the same domain as the homepage, linked
  from the homepage, and linked from the consent screen.
- The privacy policy must link Google's security settings page at
  <https://security.google.com/settings/security/permissions> and disclose how
  the client accesses, uses, stores and shares Google user data.
  <https://developers.google.com/youtube/terms/developer-policies>
- The terms must link <https://www.youtube.com/t/terms> and state that users of
  the API Client agree to be bound by it.
- If the service starts using API data in a way the accepted policy did not
  cover, the policy must be updated and users re-prompted to accept it.

## Note on the consent screen

Do not upload an app logo. On an external app with publishing status
*In production*, a logo triggers brand verification. Without one, the project
stays in Google's personal-use lane (fewer than 100 users, click through the
unverified-app warning) and needs no review.
