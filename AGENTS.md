# OceanMail Server — Agent Instructions

These repository-local instructions apply to implementation agents working in `OceanMail/oceanmail-server`.

## Organization authority

Organization-level OceanMail definition, architecture, terminology, repository inventory, cross-repository decisions, current project state, and AI/contributor workflow are authoritative in [`OceanMail/oceanmail-project`](https://github.com/OceanMail/oceanmail-project).

Before substantial Server work, read there in order:

1. `PROJECT.md`
2. `CURRENT_STATE.md`
3. `DECISIONS.md`
4. `REPOSITORIES.md`
5. `workstreams/server.md` and, when relevant, `workstreams/identity-accounts.md`
6. relevant project ADR/interface/terminology documents

Then read this repository's README/docs, current source, open PRs/issues, and tests.

## Server boundary

This repository owns Server-specific implementation for:

- hosted accounts/authentication;
- hosted mailbox/service state;
- Internet-facing OceanMail APIs/jobs;
- conventional Internet-mail/provider adapters and authorized service handoff;
- server-side quota/accounting/reconciliation implementation;
- abuse/billing/retention implementation;
- application-level Server security and recovery behavior.

It does not own Desktop UI, onboard Station/radio integration, modem behavior, HERMES/Mercury internals, or deployment infrastructure.

Do not independently redefine organization-level identity semantics, OMail delivery-state meaning, gateway/relay policy, Client/Station/Server boundaries, or product-wide accounting semantics. Surface conflicts to the project spine.

## Historical code

`OceanMail/oceanmail-server-0.1-prototype` is historical evidence, not current authority. Reuse useful authentication, queue, security, or persistence work only after deliberate review against current 0.2 architecture. Do not inherit BEMPIC/M4P assumptions or merge historical carry-forward work conceptually without porting/revalidation.

## Security and evidence

- Do not commit secrets, credentials, private keys, production tokens, customer data, or sensitive production material.
- Authentication, authorization, accounting authority, gateway acceptance, external-server acceptance, final delivery, and human reading are distinct claims.
- Fail closed where account authorization, trust, or spending authority is unknown.
- Keep the Server transport-neutral with respect to lower-layer RF/modem behavior.

## Documentation/workflow

Component implementation truth stays here. When Server work changes organization-level architecture, terminology, identity/account semantics, cross-component interfaces, Internet-mail boundary semantics, or settled policy, update `OceanMail/oceanmail-project` as well.

Separate validation into STATIC / UNIT, INTEGRATION, and LIVE / PRODUCT. Follow architecture escalation and merge authority in the central project `AGENTS.md`.