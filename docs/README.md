# OceanMail Server Documentation

This repository owns **Server-specific implementation documentation** for OceanMail 0.2.

Organization-level product semantics, cross-repository architecture, terminology, decisions, and current project state are authoritative in [`OceanMail/oceanmail-project`](https://github.com/OceanMail/oceanmail-project).

## This repository may define

- hosted account/authentication implementation;
- mailbox/storage implementation;
- Server APIs and jobs;
- OceanMail Server ↔ Station/Gateway service contracts at the implementation boundary;
- conventional Internet-mail/provider adapters;
- service-side quota/accounting/reconciliation implementation;
- billing/abuse/retention implementation;
- application-level Server security and recovery behavior; and
- Server implementation evidence/work reports.

## This repository must not independently redefine

- OMail delivery-state meaning;
- Client/Station/Server product boundaries;
- Station roles/permissions as shared product concepts;
- vessel/user/Station/account identity semantics;
- gateway/relay product policy;
- OChat product behavior; or
- organization-wide roadmap/architecture decisions.

Those belong in `OceanMail/oceanmail-project` and should be referenced here.

## Documentation precedence

For Server work:

1. accepted project decisions/architecture/interfaces in `OceanMail/oceanmail-project`;
2. this repository's current Server architecture/API/security/operations documents;
3. Server implementation plans;
4. research/work reports/history.

If an implementation requirement conflicts with project semantics, surface and reconcile the conflict rather than silently changing product behavior here.

## Expected future structure

Create files only as real implementation requires them, for example:

```text
docs/
    README.md
    ARCHITECTURE.md
    API.md
    SECURITY.md
    OPERATIONS.md
    decisions/
    work-reports/
```

Do not create empty document classes merely to mirror the project repository.

## Legacy material

`OceanMail/oceanmail-server-0.1-prototype` is historical source material. Reuse architecture-neutral implementation lessons deliberately and revalidate them against current 0.2 boundaries; do not import old transport assumptions as Server authority.

## Shared-data urgency contract

[Project ADR-008](https://github.com/OceanMail/oceanmail-project/blob/main/docs/decisions/ADR-008-four-band-scheduling-and-channel-use.md) defines Bands 0–3 and allows the Server to designate normally background shared data, such as a security update or piracy notice, for Band 1 distribution. Designations must have authenticated Server authority and validated scope/freshness; no wire/signing format is selected yet.

Station enforces the configured normal Band 1 cap (four minutes in ten is an arithmetic example, not a default), not the full-lease route-establishment exception. Promotion does not make an update Band 0 Emergency. Ordinary shared data remains Band 3 with no reserved lease share, using idle or announced broadcasts. Station owns channel scheduling and single-radio behavior; Server remains transport-neutral. This is a required future contract, not implemented production capability.
