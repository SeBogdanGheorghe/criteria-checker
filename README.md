# GitHub Pages short link — Availability Criteria Checker

`index.html` instantly redirects to the Apps Script web app. The short link
to share and bookmark is:

**https://sebogdangheorghe.github.io/criteria-checker/**

## Why a redirect and not an embed?

An iframe embed was tried first and cannot work: browsers treat the Google
session cookie as a third-party cookie on a non-Google domain and refuse to
send it, so the frame always bounces to a Google login page — which itself
refuses to render inside frames ("www.google.com refused to connect").
That is browser privacy policy and applies to all login-protected Google
apps embedded on external sites. After the redirect the address bar shows
the long `script.google.com` URL; the only way to hide it completely is an
embed on Google Sites (same Google domain, so cookies stay first-party).

## If the exec URL ever changes

A new Apps Script *deployment* (as opposed to a new *version* of the
existing one) gets a new exec URL. Update the three `script.google.com`
URLs in `index.html` (meta refresh, fallback link, script redirect), then
commit and push — the github.io link everyone uses stays the same.
