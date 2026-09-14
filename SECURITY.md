# LocalNetHealth Security Notes

Local Mode binds the dashboard to `127.0.0.1` by default. LAN Mode is an
explicit RFC1918-only opt-in that requires Admin authentication and Host/
Origin validation. HTTP is not encrypted; Internet exposure, port forwarding,
reverse proxies, and public Wi-Fi use are outside Public v1 support.

## Authentication and secrets

The default `auth_disabled` mode is an unauthenticated localhost-trust mode,
not a general authentication system. `local_session` uses salted PBKDF2
verifiers and never stores passwords in plaintext. Viewer is read-only and
state-changing APIs require Admin. Notification secrets use the Windows
current-user DPAPI store and are not written to logs, exports, or API payloads.

## External DNS probe

The external DNS probe is disabled by default. It runs only after an
administrator explicitly sets `collector.external_dns_probe_enabled=true`.
The configured hostname and interval are visible in the dashboard/API. A
`not_probed` result is informational: it is not a degraded gateway, Health
Score is unchanged, and no GatewayDegradation alert is emitted. Only an
opted-in `failed` probe can contribute a DNS failure signal.

## Reporting

For general questions and ordinary defects, use the repository's
[GitHub Issues](https://github.com/moR3y/LocalNetHealth/issues). Redact
passwords, webhook URLs, SMTP values, authorization headers, DPAPI files,
SQLite backups, and unredacted exports.

For a suspected security vulnerability, do not open a public issue. Use
[GitHub Private Vulnerability Reporting](https://github.com/moR3y/LocalNetHealth/security/advisories/new)
when it is enabled for the repository. The enabled state cannot be verified
from the published source alone and is therefore a required Human Gate before
publication. If the route is unavailable, wait for the maintainer to enable it
or obtain a private reporting route; do not disclose the vulnerability in a
public issue.

Include the build identity, Windows version, reproduction steps, and a minimal
redacted log excerpt. LocalNetHealth does not promise a support response time.
