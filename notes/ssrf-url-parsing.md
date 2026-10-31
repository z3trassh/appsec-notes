# SSRF through URL parsing gaps

## The idea

Server-side request forgery happens when the server fetches a URL the user
controls. Most defences are an allowlist, and most broken allowlists compare the
URL as a string while the HTTP client reads it as a structured URL. The two
disagree on things like:

- userinfo: `http://trusted.example@127.0.0.1/` — host is `127.0.0.1`.
- case and trailing dots: `TRUSTED.example.` may pass a check and still resolve.
- redirects: an allowed host answers with a 302 to an internal address.
- DNS: a name passes the check, then resolves to a private IP (rebinding).

## How I test it

- Point the feature at a loopback or link-local address directly.
- Wrap an allowed host in userinfo in front of an internal one.
- Host a redirect on an allowed origin that points inward.
- Watch for blind SSRF: timing differences or out-of-band callbacks.

## The fix

Parse the URL, reject userinfo and non-HTTP schemes, compare the hostname
exactly, resolve it and block non-public addresses, and disable redirects or
re-validate each hop. Best of all, connect to the validated address or send the
request through an egress proxy. See
[web-vuln-labs lab 01](https://github.com/z3trassh/web-vuln-labs/tree/main/labs/lab01_ssrf).
