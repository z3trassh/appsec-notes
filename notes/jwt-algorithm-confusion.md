# JWT algorithm confusion

## The idea

A JWT header carries `alg`. If the server uses that field to decide how to verify
the signature, the client controls the verification path. The classic case:
the server signs with RS256 (asymmetric) and publishes the public key. An
attacker sends a token with `alg: HS256`, and if the verifier then uses the
public key as an HMAC secret, the attacker can sign tokens too — the public key
is public.

## How I test it

- Read a valid token. Note `alg` and whether a public key is reachable (a JWKS
  endpoint, a `.pem`, a mobile app bundle).
- Try `alg: HS256` signed with the public key bytes.
- Try `alg: none` with an empty signature.
- Change a claim that controls access (`role`, `sub`) and see if it is honoured.

## The fix

The server pins the expected algorithm from its own config and rejects any other
header value before checking the signature. A key has one purpose. See
[web-vuln-labs lab 02](https://github.com/z3trassh/web-vuln-labs/tree/main/labs/lab02_jwt)
and [RFC 8725](https://datatracker.ietf.org/doc/html/rfc8725).
