# LocalNetHealth Privacy Notes

LocalNetHealth is a local-first Windows application. Monitoring history is
stored in local SQLite storage. The default dashboard is intended for this
PC and there is no telemetry, advertising identifier, cloud upload, or fleet
control service.

## What is collected locally

The application records gateway reachability, interface statistics,
ARP/device observations, timing, alert state, and configuration needed for
the monitoring functions. It does not record packet payloads or message
contents.

## External communication

The default configuration performs no public-hostname DNS lookup. Gateway
reachability is checked locally. An administrator may explicitly enable the
optional external DNS probe in the local configuration:

- target: the configured public hostname (default `example.com`)
- purpose: confirm DNS reachability, not upload monitoring data
- period: once per configured interval (default 300 seconds)
- states: `not_probed`, `success`, or `failed`

When disabled, the state is `not_probed`; it is not a failure, does not reduce
Health Score, and does not create a GatewayDegradation alert. The target,
purpose, and current state are shown in the dashboard/API and retained with
gateway history. The probe is never run merely because the application starts.

Other external communication occurs only when an administrator enables a
notification provider or explicitly requests an update check. Notification
providers receive only the alert/test payload selected by the administrator.
Email sending is not implemented.

## Local data and uninstall

Local data may include monitoring history, exports, operation-log summaries,
configuration, and password verifiers. Notification secrets are stored
separately in the Windows current-user DPAPI store and are not included in
portable exports.

The default uninstall choice is KEEP for monitoring history and exports. DELETE
can be selected for those records. Application files, configuration, secrets,
credential state, cache, temporary data, and other runtime state are deleted in
both modes. See the uninstall section in [USER_MANUAL.md](docs/USER_MANUAL.md)
for the public retention summary.
