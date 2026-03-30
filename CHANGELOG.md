# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Integrated `CA\Log` logging across all service classes via `CaLog` facade.
- ACME operation logging in `AcmeServer` for account creation/retrieval, order creation, order finalization, certificate download, and certificate revocation.
- Nonce validation logging in `NonceManager` for successful and failed nonce checks.
- JWS signature verification logging in `JwsVerifier` for verification success and failure.
- Challenge validation logging in `Http01Validator`, `Dns01Validator`, and `TlsAlpn01Validator` with domain and result context.
- Order lifecycle logging in `OrderProcessor` for status transitions, authorization validation, and order expiration.
- Critical error logging with exception context in all catch blocks across services.
- Added `groupesti/laravel-ca-log` ^0.1 as a required dependency.

## [0.1.0] - 2026-03-29

### Added
- Initial release of the ACME protocol (RFC 8555) server for Laravel CA.
- `AcmeServer` service implementing the full ACME protocol flow.
- `JwsVerifier` service for JSON Web Signature verification.
- `NonceManager` service for replay-nonce management with configurable TTL.
- `OrderProcessor` service for certificate order lifecycle management.
- Challenge validators: `Http01Validator`, `Dns01Validator`, `TlsAlpn01Validator`.
- Eloquent models: `AcmeAccount`, `AcmeOrder`, `AcmeAuthorization`, `AcmeChallenge`, `AcmeNonce`.
- Enum-backed status models: `OrderStatus`, `AuthorizationStatus`, `ChallengeStatus`, `ChallengeType`.
- Full ACME API routes: directory, newNonce, newAccount, newOrder, authorization, challenge, finalize, certificate download, revoke.
- JWS authentication middleware (`AcmeJwsMiddleware`) for authenticated endpoints.
- Content-type middleware (`AcmeContentType`) for ACME-specific headers.
- Events: `AcmeAccountCreated`, `AcmeOrderCreated`, `AcmeChallengeCompleted`, `AcmeOrderFinalized`, `AcmeCertificateIssued`.
- Artisan commands: `ca:acme:setup`, `ca:acme:accounts`, `ca:acme:orders`, `ca:acme:cleanup`.
- Database migrations for accounts, orders, authorizations, challenges, and nonces.
- Publishable configuration file (`config/ca-acme.php`).
- `CaAcme` facade for static access to the ACME server.
