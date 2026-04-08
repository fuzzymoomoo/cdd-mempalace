# Context Bundle: Sprint 2 Planning — Onboarding Service

**Stage:** Planning  
**Sprint:** 2  
**Date:** 2026-03-20

## Goal

Complete the onboarding flow end-to-end: account creation, email verification,
and first-login redirect. All three steps must work in sequence before sprint ends.

## Active constraints

- email verification must use the existing SendGrid integration, not a new provider
- the onboarding flow must complete in under 3 seconds on a cold start
- no new infrastructure dependencies can be added this sprint

## What to retrieve at planning stage

From `onboarding-service / decisions`:
- `use-postgresql` — session storage decision, relevant for state design
- `email-verification-approach` — if it exists from prior sprint

From `onboarding-service / incidents`:
- any prior timeout or session loss incidents

From `onboarding-service / planning`:
- sprint 1 outcomes and open items carried forward

## Known risks

- SendGrid rate limiting at high signup volume (not expected this sprint but worth noting)
- session token expiry edge case: user starts onboarding, pauses for 30+ minutes

## Open questions

- should the onboarding session expire after inactivity, and if so, what is the timeout?
- does email verification need to survive a service restart mid-flow?

## Retrieval note

This bundle is filed under `onboarding-service / planning`.
Retrieve at the start of any planning session for sprint 2 work.
Archive after sprint review and replace with sprint 3 planning bundle.
