# HealSync

A patient health dashboard with medication tracking, appointments, an AI health assistant and an emergency SOS flow, built with Next.js.

Built by Vamika Bhat, Varsha Kodi and Varun Vivek for GDG-HackGPT at Phase Shift 2025, where it placed 2nd of 25 teams. The code and interface use the working name MediCare. Varsha also hosts a copy at [varshakodi/MediCare](https://github.com/varshakodi/MediCare).

> **Prototype only.** This isn't a medical tool, and the SOS button in the interface doesn't contact anyone. Never rely on it in an emergency.

**Contents:** [What's built](#whats-built) · [API routes](#api-routes) · [Run it](#run-it) · [Project layout](#project-layout) · [Limitations](#limitations)

## What's built

The interface runs in demo mode with mock login and sample data, so it works without a database. The API routes are built separately and aren't connected to it yet.

**Interface**
- Medication schedule with doses you can mark as taken
- Appointment manager
- Health charts and a family portal
- Gemini health assistant chat
- SOS screen with emergency types
- Dark mode

**Backend**
- Sign-up and login, with Joi validation, bcrypt password hashing and JWT tokens
- Emergency alerts stored in MongoDB, each with an audit log

| Area | Tools |
|---|---|
| App | Next.js 14, React 18, Tailwind CSS, Recharts |
| Backend | Next.js API routes, MongoDB Node.js driver |
| Auth | jsonwebtoken, bcryptjs, Joi |
| AI | Google Gemini |

## API routes

| Method | Route | Purpose |
|---|---|---|
| `POST` | `/api/auth/register` | Create a patient account |
| `POST` | `/api/auth/login` | Check credentials and issue a JWT |
| `POST` | `/api/emergency/alert` | Create an emergency alert |
| `GET` | `/api/emergency/alert` | List a patient's recent alerts |

## Run it

Requires Node.js 18 or later.

```bash
npm install
cp .env.example .env.local
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) and log in with any email and password.

To try the API routes, add `MONGODB_URI` and `JWT_SECRET` to `.env.local`. For the chat, add `NEXT_PUBLIC_GEMINI_API_KEY`.

## Project layout

```text
├── lib/
│   ├── auth.js                 Password hashing, tokens and request authentication
│   ├── emergency.js            Alert creation and lookup
│   └── mongodb.js              Database connection
├── models/
│   ├── Patient.js              Patient validation
│   └── EmergencyAlert.js       Alert structure
└── src/app/
    ├── page.js                 The whole interface
    └── api/                    Auth and emergency routes
```

## Limitations

- The interface doesn't call the API routes. Its login is mocked, and its SOS confirmation is simulated.
- Twilio and SendGrid are listed as dependencies, but no SMS or email code exists yet.
- The Gemini key is used in the browser, and the chat logs its first 10 characters to the console. Don't deploy it with a real key until those calls move to the server.
- There are no automated tests, and the whole interface sits in one 1,300-line file.
