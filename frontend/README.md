# ShopBike Frontend

Frontend app for ShopBike core marketplace flow.

## Run locally

```bash
npm install
npm run dev
```

## Build

```bash
npm run build
npm run preview
```

## Lint

```bash
npm run lint
```

## Core implementation reminders

- Follow ShopBike business logic in root `README.md`
- Keep auth simple and stable (`RequireAuth`, `GuestGuard`, token in Zustand)
- Use API service layer over direct component-level API calls
- Prioritize end-to-end flow correctness over training/pattern experiments
