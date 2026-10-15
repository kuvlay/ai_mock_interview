# AI Mock Interview Platform

A Next.js and TypeScript application for role-specific interview practice, voice interviews, structured feedback, and PDF resume review.

[Live demo](https://ai-mock-interview-roan-phi.vercel.app) · [Source provenance](PROVENANCE.md)

The existing demo opens the sign-in page. Its authentication, voice sessions, and paid AI integrations were not exercised during portfolio preparation.

## Implementation

- Firebase Authentication with server-side session cookies and Firestore persistence.
- Gemini question generation based on role, level, interview type, and technology stack.
- Retell voice sessions with call lifecycle handling and webhook-driven interview feedback.
- Per-question feedback, overall scores, and persisted interview statistics.
- PDF text extraction and AI-generated resume suggestions.
- Next.js server actions and API routes, Tailwind CSS components, and Docker configuration.

## Stack

Next.js 15 · React 19 · TypeScript · Tailwind CSS · Firebase Auth · Firestore · Gemini 2.5 Flash · Retell AI · Zod

## Local development

Requirements: Node.js 20, npm, your own Firebase project and Admin credentials, a Google Generative AI key, and configured Retell agents.

```bash
git clone https://github.com/kuvlay/ai_mock_interview.git
cd ai_mock_interview
cp .env.example .env.local
npm ci
npm run dev
```

Fill in `.env.local` before starting, then open `http://localhost:3000`.

| Configuration | Purpose |
| --- | --- |
| `NEXT_PUBLIC_FIREBASE_*` | Firebase browser SDK configuration; embedded in the client bundle |
| `FIREBASE_PROJECT_ID`, `FIREBASE_CLIENT_EMAIL`, `FIREBASE_PRIVATE_KEY` | Server-only Firebase Admin credentials |
| `GOOGLE_GENERATIVE_AI_API_KEY` | Gemini question generation, feedback, and resume suggestions |
| `RETELL_API_KEY` | Server-only Retell API key |
| `NEXT_PUBLIC_RETELL_AGENT_ID` | Retell agent used for interview generation |
| `NEXT_PUBLIC_RETELL_INTERVIEW_AGENT_ID` | Optional separate interview agent |

For the Firebase private key, preserve escaped `\n` newlines in the environment variable. Configure Firebase email/password sign-in, authorized domains, and your own Firestore access rules. Retell agents and webhooks must be configured in your Retell account; the application routes are `/api/retell/create-call` and `/api/retell/webhook`.

## Build and deployment notes

```bash
npm run build
npm run start
```

Firebase client values must be available at Next.js build time. The included Docker/Compose files and Docker Hub workflow are starting configurations that require your deployment credentials and build-time environment configuration. The Docker Hub publish workflow is manual (`workflow_dispatch`) until this copy is configured with its own credentials. They are not evidence of a successful deployment from this copy. The inherited `npm run lint` command uses `next lint`; review it before use with the installed Next.js version.

## Scope and limitations

The application integrates external AI and voice services and requires their availability, credentials, and account configuration. There are no verified user-count, accuracy, conversion, or latency claims. Resume scores are AI-generated suggestions, not a measured score from an employer's ATS. Review API authorization, webhook verification, resource limits, and provider configuration before exposing a new deployment publicly.

## Provenance and license declaration

This is a clean portfolio copy of [aarish-io/ai_mock_interview](https://github.com/aarish-io/ai_mock_interview), imported at the source owner's request. Source contributor attribution is recorded in [PROVENANCE.md](PROVENANCE.md). Local IDE history and real credentials are excluded; Firebase browser configuration now comes from environment variables.

The source README declares MIT, but the imported source does not include a standalone license text. That declaration is retained here without inventing a copyright holder or granting a new license.
