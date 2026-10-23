# ClinPass — Clinical Teaching Operating System

> Turn every clinical encounter, simulated or real, into a measurable learning opportunity.

🏆 **Outstanding Pitch Award, TAU Med Hackathon 2026** (Synergy Innovate × TAU Helmsley Medical Simulation Center, challenge: *"Scaling Clinical Teaching: The Future of Medical Education"*).

🌐 **Live demo:** https://clinpass-app.pages.dev
🎬 **Film (2 min):** [watch in the browser](https://clinpass-app.pages.dev/v/film.mp4) · [media/clinpass-film.mp4](media/clinpass-film.mp4)

[![ClinPass landing page](screenshots/01_landing_hero_overview.png)](https://clinpass-app.pages.dev)

---

## The problem

Medical school enrollment grows faster than teaching capacity. There are not enough instructors, not enough teaching time, limited patient access and overloaded simulation centers. The result is unequal practice and thin, impersonal feedback. Students arrive at their clinical years less prepared than they could be.

## What ClinPass does

ClinPass is a clinical-reasoning **flight simulator** for students and a teaching **command center** for instructors.

1. The system detects a student's weak clinical skills.
2. It recommends a personalized case.
3. The student practices a voice-first encounter with a live AI patient.
4. Hidden information unlocks only with the right question, the right tone, at the right moment.
5. The student orders vitals, exams, labs and imaging, then submits a differential and a plan.
6. OSCE-style feedback with evidence, then a replay of the decisive moments.
7. The instructor gets a ready debrief guide. Faculty see cohort-level gaps.

> Most tools teach cases. ClinPass teaches the learner, supports the instructor and improves the curriculum.

## Why it is not just a chatbot

| Engine | What it does |
|---|---|
| **Hidden Concern Engine** | Sensitive information unlocks only with the right topic, tone and timing |
| **Communication Engine** | Scores *how* the student speaks: Patient Trust and Clinical Presence |
| **Intent Classifier** | Topic and tone detection (judgmental / normalizing / empathic) |
| **Scoring Engine** | 100-point, 7-domain OSCE rubric with evidence and EPA mapping |
| **Replay Engine** | Reconstructs the decisive moments of the encounter |
| **Faculty and Instructor Insights** | Cohort gaps, debrief guides, teaching-load balancing |

## The learning moment, in one example

Maya (4th year) speaks with David, 72, who came in with dizziness.

- *"Are you taking your medications properly?"* → David becomes guarded. The hidden concern stays locked. Trust drops.
- *"Many people stop or change medications because of side effects, and that is completely understandable. Has anything like that happened recently?"* → David admits he stopped his blood-pressure pill. Hidden concern unlocked. Trust rises.

Same clinical question, two completely different encounters. That difference is what ClinPass measures and teaches.

## Screenshots

| Student Flight Deck | Clinical Cockpit |
|---|---|
| ![Flight deck](screenshots/02_student_flight_deck.png) | ![Cockpit](screenshots/03_clinical_cockpit.png) |

| OSCE Replay and Debrief | Faculty Command |
|---|---|
| ![Debrief](screenshots/04_osce_replay_debrief.png) | ![Faculty](screenshots/05_faculty_command_dashboard.png) |

| Instructor Copilot | Case Builder |
|---|---|
| ![Instructor](screenshots/06_instructor_copilot.png) | ![Builder](screenshots/07_case_builder_preview.png) |

## Tech stack

**Frontend:** Vite, React 18, TypeScript, Tailwind CSS with a custom clinical design system, Radix UI primitives, lucide-react, Framer Motion, Recharts, Zustand, React Router.

**Live AI patient (Live Patient Room):**
- **HeyGen LiveAvatar** streaming avatar via `@heygen/liveavatar-web-sdk`. A Cloudflare Pages Function (`/api/liveavatar/token`) exchanges the server-side HeyGen API key for a short-lived session token, so the key never reaches the browser.
- **Fallback avatars** when the SDK is unavailable: a 3D talking head (`@met4citizen/talkinghead`) and a photo-based lip-sync avatar driven by the same speech bridge.
- **Speech in the browser:** Web Speech API for recognition with live mic metering, SpeechSynthesis for the patient voice, and a typed fallback that always works.
- **Optional local runtime** (localhost:8787) that upgrades the room to a real LLM patient (Ollama), Whisper speech-to-text and Kokoro text-to-speech. Everything degrades silently when it is not running.

**Session recording and reports:** MediaRecorder composites the patient view, the student webcam, mixed audio and live captions into one video; `ffmpeg.wasm` for processing; reports and recordings sync to **Cloudflare KV** through Pages Functions (`/api/recordings`), with local storage as fallback.

**Deterministic engines** (no API keys needed for the core loop): intent classifier, patient state machine, hidden-concern state machine, communication scoring, 100-point OSCE scoring, replay reconstruction.

**Hosting:** **Cloudflare Pages** with Pages Functions (avatar token, recordings API, and a range-capable endpoint that streams the film at `/v/film.mp4`).

**Hackathon tooling:** built in 3 days with **Claude Code** (AI-assisted development), **HeyGen** (avatar) and **Higgsfield** (film).

Architecture details: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)

## Team and my role

Team of 4 at TAU Med Hackathon 2026. I (Omer Konkol) led the full build of the product: the web application, the engines and the integration of the team's medical ideas into a working prototype in 3 days. The clinical content, the case design and the educational rubric came from the medical students on the team.

## Documentation

- [Product spec](docs/PRODUCT_SPEC.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Educational rubric](docs/EDUCATIONAL_RUBRIC.md)
- [Demo script](docs/DEMO_SCRIPT.md) and [pitch script](docs/PITCH_SCRIPT.md)
- [Design system](docs/DESIGN_SYSTEM.md)
- [Safety and privacy](docs/SAFETY_AND_PRIVACY.md)
- [Future roadmap](docs/FUTURE_ROADMAP.md)
- [README in Hebrew](README_HE.md)

## Safety and scope

For medical education and simulation only. All cases are synthetic. Not for real patient diagnosis or treatment. AI feedback is formative and requires faculty review for high-stakes assessment. This is a hackathon MVP, not a certified assessment tool.

## Limitations, honestly

- Patient responses and scoring in the core loop are deterministic, rule-based logic tuned for the demo cases, not a general medical model.
- Voice recognition uses the browser Web Speech API when available, with a typed fallback that always works.
- Cohort, instructor and progress data in the dashboards are mock data.
- In the public demo the live simulation is disabled. Use **Watch Demo** inside the Live Patient Room to see an exemplary encounter.

---

Contact: omerkol123@gmail.com · [LinkedIn](https://www.linkedin.com/in/omer-konkol-b7679b3a3) · [GitHub](https://github.com/omerkonkol)
