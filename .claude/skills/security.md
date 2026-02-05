# Security Guidelines

## Authentication & Authorization
- Never hardcode secrets/keys. Use `.env`.
- Validate all inputs on the server side.
- Use least privilege principle for API keys.

## Data Protection
- Sanitize all user inputs (prevent XSS/SQLi).
- Encrypt sensitive data at rest and in transit.
- Do not log PII (Personally Identifiable Information).

## Dependency Safety
- Audit dependencies for known vulnerabilities (`npm audit`).
- Pin dependency versions.
