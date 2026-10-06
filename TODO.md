# To do

This is a work board, not a design journal. Each entry states an outcome and the
next concrete step; supporting evidence belongs in a linked plan or reference
document. Delete an entry when it lands, rather than checking it off.

## Next Up

- [Verify Paseo's reopened-thread path](#paseo-integration).
- [Carry a turn identity through the hook protocol](#reliability-and-lifecycle).
- [Detect and surface workspace hook directories](#security-and-permission-boundaries).

## Active

### Paseo integration

- Verify the ACP method and replayed updates used after reopening a thread; then
  exercise concurrent sessions. Plan: [plans/paseo-port-verification.md](plans/paseo-port-verification.md).
- Label subagent-origin permission requests without weakening their containment
  or sticky-answer scope. Plan: [plans/ecosystem-followups.md](plans/ecosystem-followups.md).
- Establish the supported representation for native agy child agents, then
  validate ordering, lifecycle, logs, and cancellation. Plan: [plans/ecosystem-followups.md](plans/ecosystem-followups.md).
- Reproduce Paseo task-state and whole-file-revert reports before adopting any
  community-fork fix. Plan: [plans/ecosystem-followups.md](plans/ecosystem-followups.md).

### Security and permission boundaries

- Decide and implement the lifetime, inspection, and revocation model for
  remembered permission answers. Plan: [plans/permission-boundaries.md](plans/permission-boundaries.md).
- Decide whether an opt-in may use native agy permission grants, while retaining
  exact command keying, containment, and sensitive-path checks. Plan: [plans/permission-boundaries.md](plans/permission-boundaries.md).
- Detect and surface workspace hook directories before the first turn; pursue an
  upstream isolation option separately. The trust boundary itself is already
  documented in the README; what remains is the opt-in detection.
  Plan: [plans/workspace-hook-trust-boundary.md](plans/workspace-hook-trust-boundary.md).

### Reliability and lifecycle

- Decide whether global prompt serialization remains intentional; make any
  concurrency change safe for permission routing. Plan: [plans/reliability-lifecycle.md](plans/reliability-lifecycle.md).
- Carry a turn identity through the hook protocol to reject stale same-session
  requests. Plan: [plans/reliability-lifecycle.md](plans/reliability-lifecycle.md).
- Bound IPC frames, pending requests, and output buffering without introducing
  deadlock. Plan: [plans/reliability-lifecycle.md](plans/reliability-lifecycle.md).
- Verify denial/result ordering and provider-error presentation. Plan: [plans/reliability-lifecycle.md](plans/reliability-lifecycle.md).

### Fork maintenance

- Decide whether CI-based SonarCloud supplies value beyond Clippy and llvm-cov.
  Plan: [plans/fork-maintenance.md](plans/fork-maintenance.md).
- Assess replacing private-schema conversation replay with adapter-owned history.
  Plan: [plans/fork-maintenance.md](plans/fork-maintenance.md).
- Evaluate ACP configuration, per-session workspace roots, and upstream changes
  only with an explicit compatibility plan. Plan: [plans/ecosystem-followups.md](plans/ecosystem-followups.md).
- Widen the e2e model roster beyond `gemini-*-flash-low` if the CI key can call
  more distinct base models (e.g. GPT-OSS 120B, Claude Sonnet 4.6, Flash Lite);
  thinking-level variants share their base model's quota and add no headroom.
  Next: with the CI key and pinned agy, capture `agy models` and try one turn on
  each non-flash row. Reference: [quota rotation](plans/completed/e2e-quota-rotation.md).
- Make the e2e agy pin real and current: CI installs CLI 1.1.26, but its log
  reports the language server it runs as the latest release (1.2.17 on
  2026-10-05, 1.3.0 on 2026-10-06), and agy ≥1.2.12 stops retrying on a daily
  or billing quota cap instead of burning requests. Next: find agy's
  auto-update switch, then bump the pin and its SHA-256 in `e2e.yml`.

## Icebox

- Revisit a PTY fallback only if current agy versions reproduce the original
  non-TTY or thinking-model failures. Reference: [investigation notes](dev-docs/research/investigation-notes.md#pty-fallback).
- Investigate a Paseo context bridge only if required host context is unavailable
  to agy. Reference: [investigation notes](dev-docs/research/investigation-notes.md#daemon-context-bridge).
- Do not adopt the rejected community-fork designs without a new threat-model
  decision. Reference: [deferred record](plans/deferred/community-and-command-parsing.md).
