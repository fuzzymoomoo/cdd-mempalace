# Decision: Use PostgreSQL for session storage

**Status:** Accepted  
**Date:** 2026-03-15

## Context

We needed a durable store for onboarding session state that supports concurrent writes
from multiple service instances and can be queried by user ID and session ID.

SQLite was the initial candidate because it requires no infrastructure, but it cannot
handle concurrent writes from more than one process.

Redis was considered for its speed, but adds an operational dependency we are not
ready to take on and does not survive restarts without persistence configuration.

## Decision

Use PostgreSQL 15 with pgbouncer for connection pooling.

## Rationale

- handles concurrent writes correctly without application-level locking
- schema migrations via Alembic are already in use elsewhere in the stack
- the team has existing operational knowledge of PostgreSQL
- connection pooling via pgbouncer keeps connection counts manageable

## Tradeoffs accepted

- adds infrastructure complexity compared to SQLite
- requires a running PostgreSQL instance in dev (docker-compose handles this)
- slightly more setup for new contributors

## Rejected alternatives

- SQLite: cannot handle concurrent writes from multiple processes
- Redis: fast but adds persistence and ops complexity we are not ready for
- In-memory store: no durability, rules out horizontal scaling

## Retrieval note

This decision is filed under `onboarding-service / decisions`.
Retrieve during planning and implementation stages when auth or session storage is in scope.
