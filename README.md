# Velt Integration Quality

This repository owns Velt's cross-package verification strategy. Individual packages can be healthy while the framework is broken as a distribution; this project proves that tagged components install, boot and work together from a clean environment.

> Status: release infrastructure in progress. A green unit suite in one repository is not sufficient evidence for a Velt framework release.

## Responsibilities

- Define compatible tag matrices for all Composer packages.
- Test clean installations without developer worktree junctions or path repositories.
- Create real web, API and cross-platform projects through the CLI.
- Exercise HTTP, UI, database, ORM, migrations, seeders and Preview end to end.
- Run supported PHP/OS matrices and lowest/highest dependency resolution.
- Enforce source quality, security, licensing and documentation requirements.
- Execute Android bridge, Compose, APK/AAB and installation gates when native support is promoted.
- Publish test reports, hashes, dependency inventory and provenance with releases.

## Quality pyramid

```text
Package unit tests
        ↓
Package contract tests against public interfaces
        ↓
Multi-package integration sandbox
        ↓
Clean consumer projects from tags/dist archives
        ↓
Platform E2E: web server/browser and Android emulator/device
        ↓
Release artifacts, signing, SBOM and provenance
```

Fakes are valuable at the unit layer. They never replace the real package or platform at integration/release layers.

## Local multi-repository development

A maintainer sandbox may use Composer path repositories:

```json
{
  "repositories": [
    { "type": "path", "url": "../veltphp-kernel", "options": { "symlink": true } },
    { "type": "path", "url": "../veltphp-http", "options": { "symlink": true } },
    { "type": "path", "url": "../velt-ui", "options": { "symlink": true } }
  ]
}
```

This mode accelerates implementation but cannot prove a release. The final matrix removes path repositories, clears Composer caches where relevant and installs only published tags or commit-addressed public VCS prereleases.

## Minimum package gate

Every publishable repository must provide:

- valid package manifest and lock policy;
- LICENSE and user-oriented README;
- tests executable from a clean clone;
- static analysis and formatting policy appropriate to the codebase;
- CI on supported runtimes;
- changelog/upgrade note for public changes;
- dependency and security review;
- no local absolute path, secret or unintended development constraint.

## Framework scenarios

### Web

```bash
velt new smoke-web --type=web --styling=tailwind --database=sqlite --no-interaction
cd smoke-web
velt migrate
velt db:seed
composer test
npm run build
velt kernel:check
```

The gate verifies Tailwind is installed and built, web routes render, assets exist, database work succeeds and no Android-only dependency leaks into the profile.

### API

```bash
velt new smoke-api --type=api --database=sqlite --no-interaction
cd smoke-api
velt migrate
composer test
```

The gate asserts there are no views, Tailwind/Node files, Preview controllers, UI dependency or web routes, then exercises JSON and error responses.

### Cross-platform

The gate confirms NativeWind/native manifests and PHP 8.4 constraints are present while the project remains clearly marked experimental. Stable promotion additionally requires the Android matrix below.

## Android release gate

1. Build pinned PHP libraries for x86_64 and arm64-v8a.
2. Boot the real Velt kernel inside the Android process.
3. Run PHP → `nativephp_call()` → JNI/Kotlin → PHP instrumentation.
4. Render and interact with a Velt tree through Compose, not WebView.
5. Exercise permission success/denial and native error propagation.
6. Run SQLite migration and persistence after process restart.
7. Generate debug APK, signed release APK and AAB.
8. Verify signatures, alignment, manifest, permissions and bundled ABIs.
9. Install on a clean emulator and run offline/upgrade smoke tests.
10. Publish reports, hashes, SBOM and provenance.

The job checks that test doubles are absent from release artifacts and fails when an instrumented step is skipped.

## Supported matrix direction

| Layer | Matrix |
| --- | --- |
| CLI/Skeleton | Windows, Ubuntu, macOS; PHP 8.2/8.3/8.4 |
| Packages | Supported PHP lines; lowest and highest dependencies |
| Databases | SQLite, MySQL and PostgreSQL versions declared supported |
| Preview | Node LTS, protocol fixtures and Android bundle export |
| Android | min/target API, x86_64 emulator, arm64 device/device farm |

## Failure policy

Release-blocking failures include incompatible Composer tags, missing tests, security-critical advisories, unsigned or unverifiable artifacts, Android fake/WebView fallback, non-reproducible documentation and secret leakage. Flaky tests are quarantined only with an owner, issue, deadline and preserved release block when they cover a required guarantee.

## ADR and issue workflow

Cross-cutting decisions are documented as ADRs with context, chosen option, alternatives, consequences and migration impact. Work is grouped into dated milestones. Assigned issues receive automated reminders and must include progress, tests and blockers every two working days.

## Reproducing a release

A release report records repository SHAs/tags, OS/runtime/tool versions, dependency resolution, commands, test counts, skipped tests, artifact hashes and known limitations. Another maintainer must be able to repeat it without access to the original developer machine.

## Contributing

Add reusable scripts and fixtures here instead of duplicating integration logic across packages. A new public feature must add or update the scenario proving it in a clean consumer. Never weaken a gate merely to publish a tag; use an honest prerelease label until the requirement is satisfied.

## License

Documentation and automation in this repository are MIT licensed unless a file states otherwise.
