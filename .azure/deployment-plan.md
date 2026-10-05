# Deployment Plan

## Status
Implemented; not deployed

## Scope
Configure Azure Static Web Apps authentication so all served site routes require sign-in through a Microsoft Entra ID provider scoped to one tenant. Do not deploy.

## Decisions
- Hosting: Azure Static Web Apps (existing application)
- Authentication: Microsoft Entra ID provider configured with a tenant-specific OpenID issuer
- Route protection: all served routes require authenticated users
- Other sign-in providers: block GitHub sign-in
- Application settings: reference `AAD_CLIENT_ID` and `AAD_CLIENT_SECRET`; never put credential values in source control
- Deployment: not in scope

## Steps
- [x] Inspect the existing app and Static Web Apps configuration; no Static Web Apps config exists yet
- [x] Obtain the Microsoft Entra tenant ID for the issuer URL
- [x] Update route and authentication configuration
- [x] Validate the resulting configuration as valid JSON

## Deployment Notes
- Place `staticwebapp.config.json` at the site app's root (the repository root currently contains `index.html`).
- Configure `AAD_CLIENT_ID` and `AAD_CLIENT_SECRET` as application settings on the Static Web App after creating an app registration for this tenant.
- Custom authentication requires the Static Web Apps Standard plan.
- For APIs, independently validate authenticated identities before returning protected data.
