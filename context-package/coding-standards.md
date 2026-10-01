# Coding Standards

## Observed standards
- Java package names are organized by responsibility (`controller`, `service`, `entity`, `repository`, etc.).
- Classes use explicit constructors and clear naming.
- Spring annotations are applied consistently for MVC, services, configuration, and persistence.
- Records are used for DTO-like configuration (`CardProperties`, request payloads where appropriate).
- Validation is performed with Jakarta Bean Validation annotations and custom `BusinessException` errors.

## Strengths
- Source is compact and readable.
- The code is intentionally explicit and easy to follow for a demo banking service.
- The repository and service boundaries are straightforward and conventional.

## Weaknesses / risks
- There is no dedicated static analysis or style enforcement configuration in the repo beyond the standard Java build.
- Validation coverage is minimal; the single test is narrow and focused on one failure scenario.
- Some entities and utility code use compact one-line formatting, which reduces readability in a larger codebase.
- IDempotency and concurrency behavior would need stronger database-level safeguards for production use.

## Validation result
Status: WARNING

Rationale:
- The code is structurally clean and aligned with Spring conventions.
- However, operational safeguards, test breadth, and production hardening are not yet at enterprise standards.

## Environment check
The project currently fails to build in this environment because the installed Java toolchain is older than the project requirement: Maven reports `release version 21 not supported`.
