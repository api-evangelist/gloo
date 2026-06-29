# Programmatic API Onboarding — Gloo / Solo.io

A single-file, zero-dependency Node.js (18+) CLI that reproduces SoundCloud's
`sc-api-auth.mjs` pattern for Gloo / Solo.io: register an application / obtain credentials
programmatically instead of clicking through a dashboard, so agents and developers
can onboard at the command line.

- Script: [`gloo-solo-api-auth.mjs`](gloo-solo-api-auth.mjs)
- Run `node gloo-solo-api-auth.mjs --help` for usage and the required environment variables.
- Story / rationale: https://apievangelist.com/2026/07/22/gloo-platform-portal-self-serve-platform-team/

Part of the API Evangelist "Programmatic API Onboarding for the Agentic Moment" series.
