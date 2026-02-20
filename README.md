# ShopBike Core System

Core handover for implementation. This repository should follow business flow and rules below, without training-only materials.

## 1. Project Nature

ShopBike is a used-bike marketplace with inspection.

Main flow:

`Seller -> Inspector -> Buyer -> Transaction -> Sold`

## 2. Practical Tech Stack

- React + TypeScript (target stack)
- React Router v6
- Zustand
- Axios
- Tailwind CSS
- Backend REST API (`/api/...`)

No need for "UI UX Pro Max", strict academic patterns, or training-only architecture rules.

## 3. Authentication (Practical)

- Use Zustand store for `accessToken`
- `RequireAuth` for protected routes
- `GuestGuard` for guest-only routes
- Logout must clear token/state

## 4. API Layer

- Use an `apiClient`
- Request interceptor attaches token
- Refresh token flow is optional
- UI components should call API through service layer

## 5. Core Business Logic (Must Not Break)

### Publish Rule

Listing can be published only after Inspector **APPROVE**.

### Inspection Decision

Inspector outcomes:

- `APPROVE` -> Publish
- `REJECT` -> End listing flow
- `NEED_UPDATE` -> Return to Seller for edits

### Listing States

- `Draft`
- `Pending Inspection`
- `Need Update`
- `Published`
- `In Transaction`
- `Sold`
- `Cancelled`

### Editing Rule

- `Pending Inspection` -> cannot edit
- `Need Update` -> can edit
- `In Transaction` -> listing is locked

### Reserve Rule

- Reserve only after successful payment
- If transaction is cancelled, listing is unlocked again

## 6. Role System

Login can choose one role:

- Buyer
- Seller
- Inspector
- Admin

Register allows:

- Buyer
- Seller

## 7. Inspector Dashboard Requirements

- Listing queue waiting for inspection
- Listing detail page
- 3 decision actions: Approve / Reject / Need Update
- Status filter

## 8. Practical Delivery Goal

Before council/demo, full flow must run:

`Seller posts -> Inspector reviews -> Publish -> Buyer deposits -> Sold`

Priority:

- Correct business rules
- Stable auth behavior
- Clear end-to-end flow

## Out of Scope

Do not prioritize:

- UI UX Pro Max guidelines
- Git training docs
- Academic architecture checklist
- Design system generators
- Training-only documentation