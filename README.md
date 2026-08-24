# AgriCapital Frontend

AgriCapital is a digital platform for connecting agricultural projects, farmers, investors, and off-takers in Rwanda. This repository contains the **frontend application** for the AgriCapital platform.

The first frontend delivery focuses on the public entry experience and onboarding flow shown in the approved UI references:

- Welcome / marketing page
- Login page
- Investor sign-up
- Farmer sign-up
- Off-taker sign-up
- Verification page

## UI / Figma reference

> **Figma design:** Add the team's shared Figma URL here before implementation starts: `PASTE_FIGMA_LINK_HERE`

The implementation should follow the provided AgriCapital UI direction: warm off-white backgrounds, dark green brand typography, restrained gold accents, serif display headings, clean form layouts, generous spacing, and responsive desktop/mobile behavior.

The repository also contains visual references for the welcome and registration experiences. When the Figma file is available, use it as the source of truth for exact spacing, typography, component states, responsive breakpoints, icons, and interactions.

## Frontend goals for this week

By the end of the week, the frontend should provide a production-quality first-pass onboarding experience:

1. Visitors can reach the welcome page and understand the platform value proposition.
2. Users can navigate to login and the appropriate registration flow.
3. Investors, farmers, and off-takers have dedicated registration forms.
4. Forms have client-side validation, accessible labels, useful error messages, loading states, and success states.
5. Verification is implemented as a reusable page/component that can support email/phone verification from the backend.
6. The pages are responsive and visually aligned with the approved design.
7. The frontend has a clean foundation for connecting to the AgriCapital backend API.

## Tech stack

The stack is intentionally modern but lightweight so the team can move quickly without creating unnecessary complexity.

| Area | Technology | Purpose |
| --- | --- | --- |
| Framework | **Next.js + React** | Routing, rendering, application structure, and production build |
| Language | **TypeScript** | Type-safe application and API models |
| Styling | **Tailwind CSS** | Responsive styling and design-token based UI implementation |
| UI primitives | **shadcn/ui + Radix UI** | Accessible reusable primitives where appropriate |
| Icons | **Lucide React** | Consistent interface icons |
| Forms | **React Hook Form** | Performant form state and submission handling |
| Validation | **Zod** | Shared, explicit client-side validation schemas |
| Server/API state | **TanStack Query** | API requests, caching, loading/error states, and mutations |
| HTTP | **fetch / thin API client** | Backend communication without unnecessary abstraction |
| Local UI state | **Zustand** | Small cross-page state only where React state/context is insufficient |
| Fonts | **next/font** | Optimized font loading while matching Figma |
| Testing | **Vitest + React Testing Library** | Unit/component behavior tests |
| E2E | **Playwright** | Critical onboarding and navigation flows |
| Code quality | **ESLint + Prettier** | Consistent, maintainable code |
| Deployment | **Vercel or existing team deployment target** | Production hosting; final target follows team infrastructure |

### Architecture principles

- Use the Next.js App Router.
- Keep reusable UI components separate from page-level composition.
- Keep API calls in a small typed client/service layer instead of directly inside visual components.
- Keep validation schemas close to the feature and make them reusable by forms and tests.
- Do not hard-code secrets or backend credentials in the browser.
- Use environment variables for API base URLs and public configuration.
- Prefer accessible semantic HTML before adding custom interaction logic.
- Build mobile-first and verify desktop layouts against the provided references.
- Keep investor, farmer, and off-taker registration flows composable so shared fields/components are not duplicated.

## Proposed project structure

```text
src/
├── app/
│   ├── page.tsx                    # Welcome page
│   ├── login/page.tsx              # Login
│   ├── signup/
│   │   ├── investor/page.tsx       # Investor registration
│   │   ├── farmer/page.tsx         # Farmer registration
│   │   └── off-taker/page.tsx      # Off-taker registration
│   └── verification/page.tsx       # Verification
├── components/
│   ├── layout/
│   ├── navigation/
│   ├── forms/
│   ├── ui/
│   └── sections/
├── features/
│   ├── auth/
│   ├── investor/
│   ├── farmer/
│   └── off-taker/
├── lib/
│   ├── api/
│   ├── validation/
│   └── utils/
├── hooks/
└── types/
```

The exact structure can evolve as implementation begins; the important rule is to keep page composition, reusable UI, business logic, and API communication clearly separated.

## Weekly implementation issues

The following issues define the first frontend delivery. They should be implemented in dependency order and closed with the acceptance criteria documented in each issue.

### Foundation

- **Frontend foundation & design system** — bootstrap Next.js/TypeScript, Tailwind, fonts, tokens, reusable buttons/inputs/cards, responsive shell, linting, formatting, and test setup.
- **Routing & shared navigation shell** — establish routes for welcome, login, all three sign-up flows, and verification; add responsive navigation and consistent footer/header behavior.

### Public and authentication pages

- **Welcome / marketing page** — reproduce the provided AgriCapital landing page, including hero, CTAs, metrics, “How it works”, trust/compliance section, navigation, footer, responsive layout, and accessible interactions.
- **Login page** — implement the login UI, validation, password visibility behavior, loading/error/success states, navigation to registration, and backend-ready submission contract.
- **Investor sign-up page** — implement the investor registration experience with the required identity/contact fields, validation, password rules, consent, submission states, and verification redirect.
- **Farmer sign-up page** — implement the farmer registration experience using the supplied registration design direction, with farmer-specific fields, validation, responsive layout, and verification redirect.
- **Off-taker sign-up page** — implement the off-taker registration page matching the supplied design direction, including business identification, operational focus, contact details, validation, and verification redirect.
- **Verification page** — implement verification-code entry, resend behavior, countdown/disabled state, invalid-code handling, success state, and a reusable flow that can later connect to email/SMS APIs.

### Integration, quality, and delivery

- **Typed authentication API client & form integration** — connect the forms to the backend contract through a typed API layer, normalize API errors, and keep environment-specific URLs configurable.
- **Responsive/accessibility QA pass** — verify keyboard navigation, labels, focus states, contrast, error messaging, mobile layouts, tablet layouts, and desktop layouts against the reference designs.
- **Automated onboarding tests** — add component tests for validation and states plus Playwright coverage for welcome → login/signup → verification navigation and critical form behavior.
- **Frontend CI & production readiness** — add CI checks for install, typecheck, lint, tests, and build; document environment variables and local development commands.

## Definition of Done

A page is considered complete when:

- It matches the Figma/reference design closely at supported breakpoints.
- It works on mobile, tablet, and desktop.
- Interactive controls have hover/focus/disabled/loading/error/success states where applicable.
- Forms have accessible labels and clear validation messages.
- No secrets are committed to the repository.
- TypeScript, lint, tests, and production build pass.
- API integration is isolated behind the typed client layer.
- The page has a clear route and can be reached from the intended user journey.

## Local development

Once the Next.js application is initialized:

```bash
npm install
npm run dev
```

Recommended checks before opening a PR:

```bash
npm run lint
npm run typecheck
npm run test
npm run build
```

If the project uses different script names, update this section together with the package configuration.

## Backend integration

The frontend is expected to integrate with the AgriCapital backend repository:

https://github.com/tiangroupinv/agricapital-be-v1.0

Keep frontend API contracts aligned with backend authentication, user onboarding, verification, and role definitions. The frontend should not assume a backend endpoint exists until the contract is agreed and documented.

## Delivery sequence

**Day 1:** Foundation, design tokens, shared components, routing, navigation shell.

**Day 2:** Welcome page and login page.

**Day 3:** Investor and farmer registration pages.

**Day 4:** Off-taker registration and verification page.

**Day 5:** API integration, responsive/accessibility QA, automated tests, CI, and final design polish.

## Contribution

Use one branch per issue, keep commits focused, and reference the GitHub issue in pull requests. Prefer small reusable components over page-specific duplication.
