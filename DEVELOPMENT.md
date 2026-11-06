# Tado X Enhanced — Development Status

**Repository:** https://github.com/rleatherb/ha-tado-x-enhanced
**Integration domain:** `tado_x`
**Previous published release:** `v1.0.0`
**Release being prepared:** `v1.1.0`
**Status:** Release candidate validated in Home Assistant 2026.11; awaiting GitHub publication.
**Updated:** 6 November 2026

## Current development position

DEV-001 Holiday Mode implementation is included: home-level switch, status and date sensors, manual refresh, boundary handling, local date presentation, and holiday hot-water state mapping. Existing schedules, timers, history, API monitoring and multi-home behaviour are intended to remain unchanged; runtime regression testing is still required.

Stage G user testing (6 November 2026) showed that cancellation through the Tado app itself could leave hot water `OFF` instead of restoring Schedule. Home Assistant cancellation returned `AWAY_OFF` temporarily and then raw Tado API readings changed to `OFF` on the next poll. This supports, but does not conclusively prove, a Tado-side restoration issue. No automatic workaround is implemented.

The Stage C–F temporary diagnostic logging has been removed. Minimal `enabled`-only PATCH remains for toggle-only Holiday Mode changes; explicit date updates continue to use a read-modify-write request. Holiday Mode GET calls and polling cadence were not changed in this hardening pass. The potential duplicate settings read remains a future quota-conscious review item, not an untested release optimisation.

## Outstanding release gates

1. Compare with published GitHub release/tag and choose next semantic version.
2. Install candidate in Home Assistant and check both homes, entities and existing automations.
3. Regression test schedule profiles, extended climate timer, hot-water select, holiday switch/date actions, history, API monitoring and lifecycle.
4. Confirm translation wording and action UI labels in Home Assistant.
5. Accept candidate before promoting Project Sources or publishing a release.

## Development rules

1. Preserve the integration domain `tado_x`, existing config entries, entity identities, action interfaces and supported behaviour unless a change is explicitly agreed.
2. Keep all state and operations scoped to the correct Tado home, including where room IDs overlap.
3. Preserve schedule profiles, Home/Away settings, climate timers, hot water, historical data and API monitoring.
4. Avoid unnecessary Tado API calls; consider both main and schedule polling and account quotas.
5. Discuss architectural implications before implementation. Make minimal, focused changes.
6. Update `services.yaml`, `strings.json`, relevant `translations/*.json`, documentation and `CHANGELOG.md` when behaviour changes.
7. Validate Python syntax, JSON/YAML parsing, package layout, ZIP integrity and internal consistency. Record live Home Assistant/Tado API tests separately; static validation is not runtime verification.
8. Do not bump the version or publish a release without explicit approval.

## Working procedure

1. Start from the latest `Tado_X_Enhanced_Development.zip` and check its relationship to the `develop` branch.
2. Investigate an issue, agree the design, and record decisions in this file.
3. Implement minimal changes and produce complete replacement files or an updated complete development ZIP.
4. Perform and report static validation, then install and test in Home Assistant as appropriate.
5. Record test results, unresolved problems and any follow-up corrections.
6. Commit accepted changes to `develop`, with descriptive commit messages.
7. Replace the Project's development ZIP and update this file and the relevant individual documentation sources to match the accepted baseline.
8. When release scope and testing are agreed, prepare release notes, agree a semantic version, merge to `main`, tag and publish. Do not do this automatically.

## Previous investigations

The Stage C–G diagnostic builds and associated Home Assistant logs are retained separately as historical evidence, rather than copied into the release-facing changelog. See the release-readiness audit dated 6 November 2026 for detailed findings and regression matrix.
