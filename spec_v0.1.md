# Extensible Guestbook Protocol v0.1
**“Notes that outlive the notebook”**

**Status**: Draft  
**Author**: Bubby <bubby81fox@gmail.com>  
**Created**: 2026-05-19  
**License**: Public Domain / CC0

## 1. Core Principle

A guestbook belongs to a `canonical_url`, not to an `application`. If the site dies, the comments live on. Any client that implements this spec can read/write entries for any URL.

**Goal**: Eviction-proof comments. The community is the page.

## 2. Canonical URL Normalization

All guestbook entries are keyed by `canonical_url`. Clients MUST normalize URLs before read/write using these rules, in order:

1. **Lowercase** scheme and host: `HTTP://Hometown.AOL.com` → `http://hometown.aol.com`
2. **Remove `www.` prefix**: `www.geocities.ws` → `geocities.ws`
3. **Remove trailing slash**: `hometown.aol.com/~jeff/` → `hometown.aol.com/~jeff`
4. **Strip tracking params**: Remove `?utm_*`, `?fbclid`, `?gclid`, `?ref`, `?source`
5. **Strip fragments**: Remove `#section` and everything after
6. **Archive mapping**: `web.archive.org/web/[0-9]+/(http.*)` → `$1`, then re-normalize

**Examples:**