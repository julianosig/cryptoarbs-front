# cryptoarbs-front

**A SvelteKit application frontend for account, exchange and subscription workflows.** Built by [Juliano Sig](https://github.com/julianosig) with Svelte 5, TypeScript, Tailwind CSS and Lucide icons.

This repository contains the frontend. A compatible backend is required for authentication, account data and exchange integrations.

## Explore the application

| Area | Implementation |
| :--- | :--- |
| Sign-in, registration, password recovery | `src/routes/login`, `cadastro`, `recuperar-senha` |
| Authentication and route access | `src/hooks.server.js`, `src/lib/stores/auth.js` |
| Exchange credentials and operations | `src/routes/(arbify)`, `src/lib/services/exchange.ts` |
| Profile, settings and subscriptions | `src/routes/perfil`, `configuracoes`, `assinatura` |
| Reusable interface components | `src/components/forms` |
| API response and validation handling | `src/lib/utils/api.js` |
| Translation resources | `src/lib/i18n` |

## Run locally

Use Node.js 22 and npm.

```sh
git clone https://github.com/julianosig/cryptoarbs-front.git
cd cryptoarbs-front
npm install
```

Create a local `.env` file:

```dotenv
PUBLIC_API_URL=http://localhost:8000
PUBLIC_LOGO_FILE=
```

`PUBLIC_API_URL` is a public API base URL, embedded in the frontend. `PUBLIC_LOGO_FILE` must also be declared; leave it empty for the built-in fallback, or name a file served under `/assets/`. Keep API secrets out of these variables. The example assumes a backend listening locally; this repository does not start one.

```sh
npm run dev -- --host 127.0.0.1
```

Open the URL Vite prints and visit `/login`. With no backend running, the UI can load, but authentication and data requests cannot complete.

## Backend contract

The implementation includes calls to `/auth/login/`, `/auth/register/`, `/auth/reset-password/`, `/auth/me/` and exchange routes. Inspect [the services](src/lib/services) for request and response shapes. The JavaScript and TypeScript exchange services currently differ in some endpoint paths, so align the selected client with your backend.

The server hook checks a `token` cookie; the client authentication store also uses local storage. The backend must enforce authorization independently of the frontend's route checks.

## Checks and production build

```sh
npm run check
npm run lint
npm run build
npm run preview
```

`npm run check` currently reports existing type diagnostics in stores, translations, form props and pages. This documentation update does not resolve them. The project uses `adapter-auto`; choose a deployment adapter appropriate to your host. This frontend is a portfolio implementation of application workflows; screens containing example data are not evidence of live financial results.
