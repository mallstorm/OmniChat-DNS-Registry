# OmniChat DNS Registry

Public remote DNS registry for OmniChat Smart Routing.

OmniChat downloads the registry from:

`https://raw.githubusercontent.com/mallstorm/OmniChat-DNS-Registry/main/dns-registry.json`

## Active public secure DNS providers

- Comss.one DNS
- dns.malw.link
- Xbox DNS
- Astracat DNS
- GeoHide DNS
- Mafioznik DNS

The registry also records services discussed for future support that currently require
an account, client-IP authorization, a personalized endpoint, or legacy UDP/TCP DNS:
Control D Custom, DNSFlex Smart DNS, KeepSolid SmartDNS, TorGuard Smart DNS and
Smart DNS Proxy. These are catalog-only and disabled by default.

## Format

`version: 1` is the format currently supported by OmniChat.

Each usable provider has one or both of:

- `protocols.doh` — DNS-over-HTTPS URL
- `protocols.dot` — DNS-over-TLS endpoint

`domains` controls which hostnames Smart Routing considers that provider for.
`capabilities` are descriptive provider/service tags and are reserved for provider-aware
health checks and routing.

Lower `priority` values are tried first.

Set `enabled` to `false` to remotely disable a provider without releasing a new APK.

## Safety

Do not add passwords, API keys, OAuth tokens, account-specific resolver IDs, or any
other secrets to this public repository.
