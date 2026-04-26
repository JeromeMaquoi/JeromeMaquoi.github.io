# IndieWeb Compliance

This document describes the IndieWeb features added to this site and how to validate them.

## What Was Added

### 1. Identity & Discovery (`rel="me"` links)

Every page now includes `<link rel="me">` tags in the `<head>` that link this site to the owner's social profiles:

| Profile | URL |
|---------|-----|
| GitHub | https://github.com/JeromeMaquoi |
| Mastodon | https://mamot.fr/@jeromemaquoi |
| Bluesky | https://bsky.app/profile/jmaquoi.bsky.social |
| LinkedIn | https://www.linkedin.com/in/jérôme-maquoi-6a6907194 |
| ORCID | https://orcid.org/0009-0006-3576-0757 |

These are generated automatically from the `author:` section of `_config.yml`. To add or update a profile, edit the corresponding field in `_config.yml`.

For IndieAuth to verify identity via Mastodon (or any other profile), the profile on that service must also link back to this site.

### 2. IndieAuth Endpoints

The following discovery links are present in every page `<head>`:

```html
<link rel="authorization_endpoint" href="https://indieauth.com/auth">
<link rel="token_endpoint" href="https://tokens.indieauth.com/token">
```

These use the hosted [IndieAuth.com](https://indieauth.com/) service, which handles the IndieAuth flow by verifying `rel="me"` links. No custom backend is required.

A machine-readable metadata file is also served at [`/.well-known/indieauth-metadata`](/.well-known/indieauth-metadata) per the [IndieAuth Server Metadata spec](https://indieauth.spec.indieweb.org/#indieauth-server-metadata).

### 3. Webmention Endpoint

Webmention support is provided by [webmention.io](https://webmention.io/), a free hosted service. The discovery links are in every page `<head>`:

```html
<link rel="webmention" href="https://webmention.io/jeromemaquoi.github.io/webmention">
<link rel="pingback" href="https://webmention.io/xmlrpc">
```

To receive webmentions, sign in to [webmention.io](https://webmention.io/) with your site URL. Incoming webmentions can then be viewed in the webmention.io dashboard.

### 4. Micropub

No Micropub endpoint is currently configured because this site has no server-side backend. To enable posting via Micropub clients in the future, consider:

- [Netlify CMS / Decap CMS](https://decapcms.org/) with a Git backend
- [micro.blog](https://micro.blog/) as a Micropub endpoint that syndicates to this site
- A custom serverless function (e.g., on Netlify or Vercel) that accepts Micropub requests and commits posts to the repository

### 5. h-card (Microformats2)

The author sidebar on every page is marked up as an [h-card](https://microformats.org/wiki/h-card), providing structured identity information:

| Property | Description |
|----------|-------------|
| `h-card` | Root class on the author profile widget |
| `p-name` | Author's full name |
| `u-photo` | Author avatar image |
| `p-note` | Short biography |
| `p-locality` | Location (Namur, Belgium) |
| `p-org` | Employer (University of Namur) |
| `u-email` | Email address |
| `u-url` + `u-uid` | Canonical URL of the site |
| `rel="me"` | All social profile links |

### 6. h-entry (Microformats2)

Pages and posts that have a publication date are wrapped in an [h-entry](https://microformats.org/wiki/h-entry):

| Property | Description |
|----------|-------------|
| `h-entry` | Root class on the article element |
| `p-name` | Page/post title |
| `e-content` | Main content area |
| `dt-published` | Publication date (ISO 8601) |
| `u-url` | Canonical URL of the entry |

### 7. Feed Discovery

The site uses [jekyll-feed](https://github.com/jekyll/jekyll-feed) to generate an Atom feed at `/feed.xml`. A discovery link is included in every page `<head>`:

```html
<link href="/feed.xml" type="application/atom+xml" rel="alternate" title="Jérôme Maquoi Feed">
```

### 8. robots.txt

A `robots.txt` file has been added at the site root, allowing all crawlers and pointing to the sitemap.

## How to Validate

### IndieWeb Identity & rel="me"

1. Visit [indiewebify.me](https://indiewebify.me/)
2. Enter `https://jeromemaquoi.github.io` in the **"Are you on the IndieWeb?"** section
3. The tool will verify that your `rel="me"` links connect back to your social profiles

### h-card

1. Visit [indiewebify.me](https://indiewebify.me/) → **"Publish on the IndieWeb"** → **h-card**
2. Enter `https://jeromemaquoi.github.io`
3. Or use the [Microformats Parser](https://microformats.org/parser) directly

### h-entry

1. Visit [indiewebify.me](https://indiewebify.me/) → **h-entry** section
2. Enter a URL of a dated page on the site
3. Or use the [Microformats Parser](https://microformats.org/parser)

### IndieAuth

1. Visit [indieauth.com](https://indieauth.com/)
2. Enter `https://jeromemaquoi.github.io` to sign in
3. The service will verify the `rel="me"` links and `rel="authorization_endpoint"` discovery

### Webmentions

1. Visit [webmention.rocks](https://webmention.rocks/)
2. Use the test suite to verify your webmention endpoint is discoverable and accepts incoming webmentions
3. Sign in to [webmention.io](https://webmention.io/) to manage received webmentions

### Microformats Parsing

Use the [Microformats2 Parser](https://microformats.org/parser) or [php.microformats.io](https://php.microformats.io/) to parse and inspect the structured data on any page.

## Configuration

All social profile URLs used for `rel="me"` links are configured in `_config.yml` under the `author:` key. Update the relevant fields there to add or change profiles.

To configure the webmention.io service:
1. Go to [webmention.io](https://webmention.io/) and sign in with `https://jeromemaquoi.github.io`
2. The service will detect the `rel="webmention"` endpoint automatically
