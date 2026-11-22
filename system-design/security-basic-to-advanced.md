# Security: Basic to Advanced

Read these first; this file adds only what they don't cover:

- [System design questions](questions.md): auth, JWT HS256 vs RS256, CORS, CSRF, sessions, OAuth2, OpenID, SSO, TLS
- [Tech lead mock interview](../java/techlead-mock-interview.md): symmetric vs asymmetric, hashing vs encryption, storing secure data, microservice logout, OAuth2 vs OIDC
- [Senior developer topics](senior-dev.md): token revocation, key rotation, secrets, zero trust, mTLS
- [React questions](../js_nodeJs/react/questions.md): token storage, CSRF and XSS prevention

## Basic

1. How do you store passwords?
   - A slow salted hash: Argon2id or bcrypt. Never plain SHA-256.
2. What is SQL injection and how do you prevent it?
   - Parameterized queries or an ORM; never build SQL by string concatenation.
3. What is clickjacking and how do you prevent it?
   - Another site frames yours and tricks the user into clicking. Send `Content-Security-Policy: frame-ancestors 'self'`.

## Intermediate

1. Which OAuth 2.0 flow for a SPA, a mobile app and service-to-service calls?
   - Authorization code with PKCE for SPA and mobile. Client credentials for service-to-service.
2. Role-based vs attribute-based access control?
   - RBAC checks the user's role. ABAC checks attributes of the user, resource and context, for example "owner of this order".
3. What is IDOR (broken object level authorization)?
   - `GET /orders/42` returns someone else's order because the API checks login but not ownership. Check ownership on every object.

## Advanced

1. TOTP vs WebAuthn passkeys for MFA?
   - TOTP shares a secret and can be phished. Passkeys use public-key crypto bound to the site origin.
2. What is SSRF and how do you prevent it?
   - The server fetches a URL the attacker chose. Allow-list hosts, and block internal ranges and cloud metadata addresses.
3. How do you protect against brute force and credential stuffing?
   - Rate limits per account and IP, breached-password checks, MFA, and alerts on login failure spikes.
4. How do you handle PII and data privacy (GDPR) requirements?
   - Data minimisation, masking in logs, retention limits, the right to delete, and audit trails.

## Scenario

1. A JWT signing key leaked. What do you do in the next hour?
2. A penetration test finds stored XSS in comments. How do you fix it and stop it coming back?
3. Design login for a web app, a mobile app and a public API using one identity provider.
