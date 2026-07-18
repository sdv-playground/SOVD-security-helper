# SOVD-security-helper — RETIRED (2026-07-19)

This service is retired and receives no further changes.

It was built for an auth model that no longer exists: an offboard microservice
holding per-ECU UDS SecurityAccess secrets, computing seed→key responses so a
*client* (SOVD Explorer, `sumo-campaign`) could unlock an ECU over SOVD before
flashing. The stack has since converged on:

- **Client → SOVD authorization = JWT bearer tokens** (workshop/onboard
  minters; see `docs/design/authorization.md` in the workspace).
- **UDS SecurityAccess = the SOVD server's job**, performed transparently
  onboard on an authorized request, via a per-ECU `UnlockProvider` seam in
  `sovd-uds` (the dev provider implements the same XOR derivation this
  service offered as `algorithm = "xor"`).

Nothing should talk to :9100 anymore. If you are looking for device unlock,
configure the ECU's `unlock` section in the SOVD server; if you are looking
for operator credentials, see `sovd-token-helper`.
