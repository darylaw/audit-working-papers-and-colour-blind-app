# Confidentiality verification

The four identified application defects were addressed in this version:

| Finding | Change |
|---|---|
| CONF-001: trial balance persisted with engagement settings | Removed engagement/profile persistence and legacy restoration; clears old application audit-storage keys without reading their contents |
| CONF-002: sign-out lacked explicit cleanup | Added an export reminder and end-session flow; clears memory, rendered content, input timers and pending readers; signals other open app tabs and handles pagehide/pageshow |
| CONF-003: CGU name inserted as HTML | Escapes the dynamic name and uses a shared renderer that never inserts parsed HTML |
| CONF-004: forecast heading inserted as HTML | Escapes the heading, with the same shared rendering defence |

Additional protection: exact script hashes replace permissive inline/same-origin script execution. Script attributes, data connections, workers, frames, forms and remote image loads are blocked. The hosted response and embedded page use the same policy.

83 automated checks cover memory-only state, legacy cleanup, pending-import cancellation, cross-tab signalling, restored pages, hostile markup, both module notes and script hashes. Hosted-route tests reject request bodies without reading them. Local Chrome verification observed hostile entity text displayed literally with no image element created. A fictitious trial balance imported 83 records; applying engagement settings did not populate a newly opened tab. Ending the session cleared both open app tabs, and reload returned a blank engagement. No console errors were captured in those checks.

This is targeted verification, not an independent penetration test. Full live network capture, independent browser-profile authentication tests, hosted multi-tab sign-out and all browser-restoration variants are not yet verified. Platform-injected infrastructure behavior is outside the source-only checks. Use fictitious data until that validation and the known accuracy defects are resolved.

Older already-open versions cannot be rewritten remotely. Export anything needed, then close old app tabs and open the updated version so its cleanup runs. Exported files remain on the user's device and are outside browser-session cleanup.

Report security issues without posting client data, uploaded schedules, credentials, or financial records. Use a minimal fictitious reproduction.
