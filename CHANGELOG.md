# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

- **Python support**: minimum is now 3.12 (`requires-python = ">=3.12"`); CI matrix
  moved from 3.10–3.12 to 3.12–3.13 (3.10 is end-of-life). `.python-version` pins
  3.13 and the Docker image uses `python:3.13-slim`.
- **CI**: GitHub Actions pinned by commit SHA, `timeout-minutes` on every job, and a
  new `docker-build` job that builds the image (no push).
- **Dependabot**: weekly grouped minor/patch updates for pip, monthly grouped
  updates for GitHub Actions, and a new `docker` ecosystem for the base image.
- **SECURITY.md**: Private Vulnerability Reporting is now enabled; the contact
  email is stated explicitly.

### Fixed

- `requirements.txt` was encoded as UTF-16LE (despite its own comment saying
  UTF-8), which made Dependabot fail with `dependency_file_not_evaluatable`.
  It is now UTF-8 with LF line endings.

### Added

- `.editorconfig`, `.github/CODEOWNERS` and the `fix-byte-order-marker` /
  `mixed-line-ending` pre-commit hooks.

## [1.0.0] - 2026-06-11

Initial professional release of **Flask Security Lab**, an educational Red Team
vs. Blue Team security lab.

### Added

- **Application-factory Flask app** (`create_app()`) with a `src/` layout, a
  central vulnerability catalog, and configuration objects.
- **10 mirrored vulnerabilities** implemented as paired `vulnerable/` and
  `secure/` modules so learners can diff the flaw against its fix: SQL
  injection, XSS, SSTI, command injection, path traversal, IDOR, SSRF, insecure
  deserialization, JWT authentication flaws, and brute force. Together these
  cover **7 of the OWASP Top 10** categories.
- **Blue Team layer**, toggled by the `BLUE_TEAM_ENABLED` flag, providing:
  structured JSON logging, signature-based attack detection, a mini-WAF,
  security response headers, and rate limiting.
- **Loopback-only Red Team attack CLI** (`src/red_team`) with automated
  exploits and a safety guard that restricts targets to `127.0.0.1`/localhost.
- **Full pytest suite** covering both attack (against vulnerable code) and
  defense (against secure code and the Blue Team layer).
- **Docker & Docker Compose** support for one-command setup (`docker compose
  up`).
- **GitHub Actions CI** running on push and pull request to `master`.
- **Pre-commit hooks** (ruff, black, mypy) enforcing the quality gate.
- **Bilingual documentation** (English/Portuguese) with per-vulnerability
  walkthroughs.

[Unreleased]: https://github.com/limarios/flask-security-lab/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/limarios/flask-security-lab/releases/tag/v1.0.0
