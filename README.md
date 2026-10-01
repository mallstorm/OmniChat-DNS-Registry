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


## Smart Routing v2

OmniChat 0.8.69+ can use optional `probes` metadata from each provider to test a
resolver separately for each AI service. A probe performs DNS resolution through that
resolver, a TLS handshake to the target service and an anonymous HTTPS reachability
check. No API keys, OAuth tokens, cookies or chat content are sent.

Example:

```json
"probes": {
  "gemini": [{"host": "gemini.google.com", "https": true}],
  "openai": [{"host": "chatgpt.com", "https": true}],
  "github_copilot": [{"host": "api.githubcopilot.com", "https": true}]
}
```

The app combines availability, DNS latency, TLS latency, HTTP reachability, jitter and
real transport failures into a per-network, per-service route score. A small registry
`priority` bias remains, but it no longer overrides clearly better measured routes.

Optional `bootstrap_ips` may be added to a resolver profile when the system DNS cannot
resolve the resolver hostname itself. TLS certificate validation and SNI still use the
original resolver hostname.
