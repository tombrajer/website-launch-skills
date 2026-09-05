# Audit Checklist

Use this as a coverage guide, not a mechanical pass/fail list. Skip irrelevant items and explain why.

## Security and access

- Secrets absent from source, history, frontend bundles, logs, and public configuration
- Production keys differ from test/development keys
- Server-side authorization covers roles, ownership, tenant boundaries, and object-level access
- Database policies deny access by default
- Privileged service keys never reach clients
- Sessions expire, rotate, revoke, and use secure cookie/token storage
- Login, reset, verification, invitation, and recovery flows resist enumeration and replay
- Sensitive state changes have CSRF protection when cookie-authenticated
- Inputs are validated server-side; outputs are contextually encoded
- Queries and commands are parameterized
- URLs and outbound requests resist SSRF and open redirect abuse
- Uploads restrict type, size, name, destination, access, and processing
- Public identifiers do not substitute for authorization
- Rate limits cover auth, email, search, writes, uploads, payments, and expensive endpoints
- Security headers are appropriate and CSP is practical, not decorative
- CORS is allowlisted and credential behavior is deliberate
- Errors do not expose stack traces, SQL, paths, secrets, or internal identifiers
- Debug/admin/test routes and default accounts are removed or protected
- Dependencies and build pipeline are reviewed for supply-chain risk

## Payments and entitlements

- Price and product selection are server-authoritative
- Payment provider signatures are verified
- Webhook processing is idempotent and replay-safe
- Event ordering and duplicate delivery are handled
- Entitlements derive from durable provider/server state
- Failed, disputed, refunded, expired, canceled, and past-due states are handled
- Client redirects are not trusted as payment confirmation
- Test mode and production mode cannot be confused
- Refund, tax, invoice, and cancellation behavior matches displayed promises

## Data and privacy

- Collected data is necessary and documented
- Retention and deletion behavior exists
- Account deletion handles dependent records, storage, auth, and billing
- Logs and analytics avoid unnecessary sensitive data
- Backups are protected and covered by retention/deletion policy
- Export and portability behavior is considered
- Third parties and subprocessors are documented
- Consent and unsubscribe behavior is functional

## Reliability and operations

- Production build succeeds from a clean checkout
- Lockfiles and runtime versions are pinned
- Required environment variables fail fast with clear errors
- Migrations are repeatable, ordered, and safe for existing data
- Rollback is practical
- Backups exist and restore has been tested
- Monitoring covers frontend, backend, jobs, database, payments, and email as relevant
- Alerts reach an accountable person
- Logs include correlation context without leaking secrets
- Timeouts, retries, idempotency, and circuit-breaking are appropriate
- Background jobs survive retries and duplicate execution
- Health checks reflect real dependency health without leaking internals
- Capacity and service limits are understood

## Product behavior

- Core journeys work on fresh, existing, expired, banned, and unauthorized accounts
- Every mutation has a visible success or failure outcome
- Empty, loading, error, timeout, and offline states are usable
- Email links expire and behave correctly when reused
- Race conditions and double submission do not corrupt state
- Users cannot manipulate scores, ranks, inventory, roles, rewards, or entitlements from the client
- Moderation/reporting exists where user-generated content creates risk
- Support and recovery paths are visible

## Accessibility, SEO, and performance

- Keyboard access and visible focus work
- Inputs have programmatic labels and errors
- Headings and landmarks are meaningful
- Contrast and zoom remain usable
- Motion can be reduced where needed
- Page titles and descriptions are unique
- Canonical, robots, sitemap, and social metadata are correct
- Private pages are not accidentally indexable
- Images have dimensions, appropriate formats, and useful alternative text
- Caching and compression are configured
- Large bundles, blocking resources, and slow queries are identified
- Core pages remain usable on realistic mobile networks
