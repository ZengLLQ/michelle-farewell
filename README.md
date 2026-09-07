# Farewell Michelle

A personal farewell letter for Michelle, presented with a purple palette, glass cards, a 3D background, and reading animations. Built with React as a single-page reading experience for desktop and mobile.

## Features

- Opening section with animated text and a scroll hint.
- Seven letter paragraphs that appear as they enter the viewport.
- A 3D background with organic shapes, particles, and colors and camera movement that respond to scrolling.
- Glass cards with mouse tilt, click/tap sparkles, and smooth scrolling.
- Reading progress indicator and a handwritten-style signature.

## Quick start

Install Node.js and Yarn Classic **1.22.22**, matching the frontend's package manager declaration. The repository does not pin a Node version. From the project root, run in PowerShell:

```powershell
cd frontend
yarn install --frozen-lockfile
yarn start
```

Open [localhost:3000](http://localhost:3000). The root has no `package.json`; run Yarn from `frontend` using `frontend/yarn.lock`.

The current page does not require the backend, MongoDB, or frontend environment variables. The letter content is stored in React components.

## Documentation

| Guide | Contents |
| --- | --- |
| [Development](docs/DEVELOPMENT.md) | Setup, architecture, configuration, builds, verification, and troubleshooting |
| [Customization](docs/CUSTOMIZATION.md) | Editing the letter, names, colors, and animations |
| [Optional backend](docs/BACKEND.md) | Python/MongoDB setup, environment variables, and API |
| [Frontend](frontend/README.md) | Frontend command reference |

## Project structure

```text
farewell-michelle/
├── frontend/
│   ├── public/index.html     # HTML, metadata, external scripts
│   ├── src/App.js            # Page composition and scrolling
│   ├── src/components/      # Content and visual effects
│   ├── src/components/ui/   # Supporting UI components
│   ├── craco.config.js      # Aliases and development server
│   ├── package.json
│   └── yarn.lock
├── backend/
│   ├── server.py            # FastAPI and status storage
│   ├── requirements.txt
│   └── pytest.ini
├── docs/                    # Project guides
├── memory/PRD.md             # Initial requirements notes
├── design_guidelines.json    # Design reference
└── test_result.md            # Historical testing notes
```

## Technology

| Area | Stack |
| --- | --- |
| UI | React 19, Tailwind CSS 3 |
| Animation | Framer Motion 11, Lenis |
| 3D | Three.js, React Three Fiber, Drei |
| Tooling | react-scripts 5, CRACO 7, Yarn Classic |
| Optional backend | FastAPI, Pydantic, Motor, MongoDB |

## Production build

From the `frontend` directory:

```powershell
yarn build
```

The output is in `frontend/build/` for static hosting. See the [hosting guide](docs/DEVELOPMENT.md#build-and-hosting). The repository does not specify a production deployment URL.

## WebStorm

Choose **File > Open** and open the `farewell-michelle` root directory. Open `README.md` to navigate the documentation. Run frontend commands in the integrated terminal, or create a run configuration for the `start` script in `frontend/package.json`.

## Implementation status

The frontend is not connected to the backend. There is no login, letter submission form, or content editor. The HTML loads Emergent scripts and initializes PostHog; fonts are loaded from Google Fonts. The frontend is not fully offline even though it does not use the local API.

This documentation describes the current code. The PRD and historical test notes do not establish that every plan or test has been implemented in the current version.
