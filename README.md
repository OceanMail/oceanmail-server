# OceanMail Server

OceanMail Server is the hosted-service and authoritative public Internet-mail application boundary for OceanMail 0.2.

## Authority and scope

Organization-level OceanMail definition, architecture, cross-repository decisions, terminology, repository inventory, and current project state are authoritative in [`OceanMail/oceanmail-project`](https://github.com/OceanMail/oceanmail-project).

This repository owns hosted accounts/authentication, mailbox/service integration, outgoing/incoming public Internet-mail handoff, quotas/accounting implementation, abuse controls, billing boundaries, and Server-side APIs/jobs.

It does **not** own Desktop UI, onboard Station/radio integration, modem behavior, HERMES internals, or deployment infrastructure.

Start with root [`AGENTS.md`](AGENTS.md), [`docs/README.md`](docs/README.md), central [`workstreams/server.md`](https://github.com/OceanMail/oceanmail-project/blob/main/workstreams/server.md), and project ADR-006.

## 0.2 boundary

```text
native OMail / OceanMail Desktop / Station / authorized Gateway
    -> authenticated OceanMail service boundary
    -> OceanMail Server
    -> centralized public SMTP/MX boundary
    -> conventional Internet mail/services
```

OceanMail-operated Server/infrastructure is the only public Internet SMTP/MX boundary. Internet-connected Stations and gateway Stations do not independently deliver to arbitrary public SMTP systems and are not public MTAs merely because they have Internet connectivity or local Postfix capability. They exchange eligible OMail traffic with Server through the accepted authenticated OceanMail service boundary.

Native boat-to-boat/store-carry-forward OMail remains decentralized and does not require Server or Internet availability. If Server is temporarily unreachable, Internet-boundary work may be delayed and retried while viable native OMail paths continue.

Station-side HERMES/Mercury integration belongs in `OceanMail/oceanmail-station`. Server should remain transport-neutral enough that an authorized OceanMail request may arrive through HF-derived gateways, IP, cellular, satellite, or other supported paths without embedding modem/radio behavior here.

The architectural SMTP/MX authority is settled; exact production provider, host count, geographic placement, IP allocation, reputation operations, and scale-out/HA design remain implementation/deployment decisions.

## Legacy prototype

The previous implementation is preserved in `OceanMail/oceanmail-server-0.1-prototype`. Useful authentication, queue, persistence, and security work may be deliberately ported after review; the active 0.2 Server does not inherit that repository's architecture automatically.

## Immediate milestone

Define and implement the narrow authenticated service contracts required for real 0.2 end-to-end operation, including Station/Server and direct-client/Server paths, while coordinating account/identity semantics with the Station and preserving truthful external-mail evidence.

Public-mail implementation must eventually cover durable SMTP/MX ingress/egress, destination retry, bounce handling, DKIM/SPF/DMARC alignment, reputation, abuse/rate controls, and operational evidence without distributing public-MTA responsibility to Stations.

Security, licensing, provider, and deployment decisions must remain explicit before production/public release.

## Publication preparation

This is an experimental bootstrap, not a production-ready implementation. See [CONTRIBUTING.md](CONTRIBUTING.md), [SECURITY.md](SECURITY.md), and [Project #42](https://github.com/OceanMail/oceanmail-project-archive/issues/42). The approved source/documentation licenses are installed. See [LICENSING.md](LICENSING.md) and [PUBLICATION.md](PUBLICATION.md). Additional inbound contribution terms remain unadopted; administrator settings and fresh hosted checks require verification.

## Licenses

OceanMail-owned code and validation tooling: [AGPL-3.0-only](LICENSE). Documentation: [CC-BY-SA-4.0](LICENSE-DOCS). See [scope](LICENSING.md) and the [fresh-history boundary](PUBLICATION.md).
