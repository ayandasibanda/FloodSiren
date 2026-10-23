# 🌊 FloodSiren
### Turning Flood Risk Into Warnings People Can Act On

**FNB App of the Year Hackathon 2026** | Climate Resilience & Essential Services

FloodSiren is a dual-channel hydro-risk early warning platform designed to help vulnerable rural and peri-urban communities in South Africa understand local flood threats and respond before conditions become dangerous.

By combining environmental risk indicators, community-reported incidents, visual alerts, and a feature-phone-oriented USSD experience, FloodSiren aims to bridge the gap between raw weather data and actionable public safety information.

> **Our mission:** Make flood-risk information understandable, accessible, and actionable, regardless of the device a person owns or the connectivity available to them.

---

## 📌 Table of Contents

- [The Problem](#-the-problem)
- [Our Solution](#-our-solution)
- [Key Features](#-key-features)
- [How It Works](#-how-it-works)
- [Technology Stack](#️-technology-stack)
- [System Architecture](#️-system-architecture)
- [Team and Responsibilities](#-team-and-responsibilities)
- [Security and SSDLC](#-security-and-ssdcl)
- [Getting Started](#-getting-started)
- [Demo and Testing](#-demo-and-testing)
- [Business and Sustainability Model](#-business-and-sustainability-model)
- [Limitations and Future Roadmap](#-limitations-and-future-roadmap)
- [Contributing](#-contributing)
- [Team FloodSiren](#-team-floodsiren)

---

## 🌧️ The Problem

Flooding can develop rapidly in communities situated near rivers, streams, low-lying roads, and vulnerable catchment areas.

Although conventional weather services provide useful information, metrics such as rainfall probability and precipitation volume do not always communicate what those measurements mean for a person's immediate surroundings.

For a resident living near a river, knowing that 35 mm of rain has fallen is less immediately useful than understanding whether local conditions indicate elevated flood risk, which roads may be affected, and what precautions to take.

The consequences of delayed or inaccessible warnings can include:

- Loss of life and injuries.
- Flooded homes and damaged infrastructure.
- Unsafe river crossings and submerged roads.
- Disrupted access to healthcare, education, and essential services.
- Limited access to timely warnings in communities with unreliable internet connectivity.

**The challenge is not only detecting environmental risk. It is translating that risk into information people can understand and act on in time.**

## 🛡️ Our Solution

FloodSiren translates environmental indicators and community observations into an accessible flood-risk experience.

The platform is designed around two complementary access channels:

1. **Web Dashboard:** Visual risk indicators, plain-language alerts, and community incident reporting.
2. **Feature-Phone Experience:** An interactive USSD-style simulator demonstrating how residents could check local flood-risk information through a simplified menu without navigating a conventional smartphone application.

The architecture is designed to support future integration with operational SMS and USSD services, subject to telecom-provider access and deployment requirements.

---

## 🚀 Key Features

### 1. 📊 Visual Hydro-Risk Engine

FloodSiren transforms environmental measurements into clear visual indicators and plain-language explanations.

- 🟢 **Green — Low Indicated Risk:** No elevated risk indicated by the available inputs.
- 🟡 **Yellow — Elevated Risk:** Conditions warrant caution and continued monitoring.
- 🔴 **Red — High Indicated Risk:** Potentially dangerous conditions require urgent attention and appropriate safety precautions.

The risk engine is designed to consider available inputs such as rainfall, water levels, terrain characteristics, and community observations.

Risk classifications are indicative and depend on the quality, freshness, and completeness of the available data.

### 2. 📱 Feature-Phone USSD Experience

FloodSiren includes an interactive, on-screen USSD-style simulator based on the proposed access code `*120*123#`.

The experience demonstrates how a resident using a basic mobile phone could navigate a simple menu to:

- Check the flood-risk status for a supported area.
- Read a short, understandable warning.
- Access basic safety guidance.

The simulator demonstrates the intended user experience. It does not, by itself, establish a live telecom connection or deliver real USSD sessions.

### 3. 📩 SMS Early-Warning Readiness

FloodSiren is designed with a future SMS notification channel in mind.

Potential capabilities include:

- Localized warnings for registered communities.
- High-priority notifications when risk thresholds are met.
- Short safety instructions suitable for basic mobile phones.
- Updates when an incident or risk classification changes.

Actual SMS delivery requires a configured messaging provider, appropriate credentials, and a tested delivery workflow. Until that integration is operational, SMS functionality should be treated as planned rather than live.

### 4. 📍 Real-Time Community Incident Reporting

Community members can contribute local observations that may help identify developing hazards.

Example reports include:

- Rising river levels.
- Submerged or damaged roads.
- Flooded pedestrian crossings.
- Blocked drainage channels.
- Other potentially hazardous local conditions.

Reports are intended to synchronize through Firebase Firestore, allowing the dashboard to reflect newly submitted information.

Reports should include timestamps and locations where available. Because community observations may be incomplete or unverified, they must be distinguished from confirmed official warnings.

### 5. 🧠 Predictive Risk Engine

FloodSiren includes a Python-based risk-engine component designed to evaluate environmental inputs and produce interpretable risk assessments.

Potential inputs include:

- Rainfall volume in millimetres.
- Water-level measurements, where available.
- Terrain slope and catchment characteristics.
- Recent rainfall trends.
- Time-stamped community observations.

The engine is designed to return a risk classification, a numerical score where supported, and an explanation of the factors contributing to the assessment.

Reliable flood-arrival-time predictions require suitable hydrological data, validated models, and local calibration. Any estimated overflow time shown in a prototype must be identified as simulated or experimental unless it has been independently validated.

---

## 🔄 How It Works

1. **Collect Inputs:** Receive available environmental measurements, test data, or community incident reports.
2. **Evaluate Risk:** The Python engine processes supported inputs and applies the configured risk-assessment logic.
3. **Store and Synchronize:** Firebase Firestore stores relevant records and supports real-time updates where configured.
4. **Communicate Risk:** The web dashboard displays understandable risk indicators and relevant incident reports.
5. **Extend Accessibility:** The USSD-style interface demonstrates a simplified feature-phone access channel, with operational telecom integration planned separately.

The goal is to turn fragmented environmental information into a clearer picture of local risk.

---

## 🛠️ Technology Stack

| Component | Technology | Responsibility |
|---|---|---|
| Frontend | Next.js App Router | Web application and routing |
| UI and Styling | React, Tailwind CSS | Responsive layouts and reusable components |
| Backend API | Python, Flask | Risk calculations and API endpoints |
| Database | Firebase Firestore | Incident storage and real-time data synchronization |
| Authentication | Firebase Authentication | User identity and access control where configured |
| Deployment | Vercel | Frontend hosting and deployment |
| Version Control | Git and GitHub | Source code and collaboration |
| Feature-Phone Demonstration | React USSD-Style Simulator | Interactive demonstration of the proposed USSD experience |

---

## 🏗️ System Architecture

```text
             ENVIRONMENTAL INPUTS
       Rainfall / Water Levels / Test Data
                        |
                        v
              PYTHON RISK ENGINE
           Input Validation and Scoring
                        |
                        v
                 FLASK REST API
                        |
                        v
                FIREBASE FIRESTORE
                 /              \
                v                v
        NEXT.JS DASHBOARD   INCIDENT REPORTS
        Visual Risk Status   Community Reports
                |
                v
       USSD-STYLE SIMULATOR
       Simplified Risk Lookup

       FUTURE INTEGRATION
       SMS Provider / Live USSD Gateway
```

### Integration Principles

- Use structured JSON contracts between the frontend and backend.
- Validate API inputs and outputs.
- Use consistent risk-status values across all interfaces.
- Store timestamps in a consistent format.
- Keep credentials and server-only secrets outside the public frontend bundle.
- Handle unavailable, stale, or incomplete environmental data explicitly.
- Separate simulated demonstration data from verified live data.

---

## 👥 Team and Responsibilities

### Ayanda Sibanda — Backend, Database & Predictive Data Lead

Responsible for backend logic, risk-engine development, data handling, and security.

- Python risk-scoring engine and analytics.
- Flask API endpoints and request validation.
- Firebase Firestore integration and data modelling.
- Firebase Authentication and access-control configuration.
- SSDLC documentation and backend security.
- Integration contracts and backend testing.

### Selemani Ecasa — Frontend, UI/UX & Product Lead

Responsible for the user-facing experience and product presentation.

- Next.js App Router application structure.
- React components and Tailwind CSS styling.
- Visual hydro-risk gauges and plain-language warnings.
- Interactive USSD-style phone simulator.
- Community incident-reporting interface.
- Responsive design, accessibility, and frontend integration.

**Collaboration Approach:** Both team members develop in parallel using agreed API contracts, shared data definitions, and incremental integration testing.

---


## 💻 Getting Started

### Prerequisites

Install the following tools before starting local development:

- Node.js and npm.
- Python 3 and pip.
- Git.
- A Firebase project with the services required by your implementation.

### 1. Clone the Repository

Replace the placeholder with the team's actual public GitHub repository URL.

```bash
git clone https://github.com/ayandasibanda/FloodSiren.git
cd FloodSiren
```

### 2. Install Frontend Dependencies

```bash
npm install
```

### 3. Configure Frontend Environment Variables

Create a `.env.local` file in the project root using the variable names expected by your Firebase configuration.

```dotenv
NEXT_PUBLIC_FIREBASE_API_KEY=your_firebase_api_key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_firebase_auth_domain
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_firebase_project_id
```

Add any additional variables required by the actual application. Do not place privileged service-account credentials in public frontend variables.

### 4. Start the Frontend

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### 5. Configure the Python Backend

If the Flask backend is maintained in a separate directory, navigate to that directory and create a virtual environment.

**Windows:**

```bash
python -m venv .venv
.venv\Scripts\activate
```

**macOS or Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the backend dependencies from the project's requirements file if one exists:

```bash
pip install -r requirements.txt
```

Configure the backend environment variables and Firebase server credentials according to the project's implementation.

Start the Flask application using the project's configured entry point. For example, if the application module is `app.py`:

```bash
flask --app app run --debug
```

The Flask development server is for local development only. Use an appropriate production server for deployment.

### 6. Connect Frontend and Backend

Configure the frontend's server-side API base URL to point to the Flask service in development and to the deployed backend in production.

The frontend and backend must agree on endpoint paths, request fields, response schemas, and error formats. The exact configuration depends on the current repository structure.

---

## 🧪 Demo and Testing

The demonstration should show the user journey from risk information to an understandable action.

### Recommended Demo Sequence

1. Open the FloodSiren dashboard.
2. Select a supported demonstration location.
3. Show a low-, elevated-, or high-risk scenario.
4. Explain the environmental inputs contributing to the displayed status.
5. Submit a community incident report.
6. Demonstrate how the dashboard reflects the new report.
7. Open the USSD-style simulator and navigate the simplified risk lookup.
8. Explain how a production deployment could connect to live environmental data and an operational SMS/USSD provider.

### Suggested Test Scenarios

- Low-risk environmental inputs.
- Heavy rainfall with elevated water-level inputs.
- Missing or stale environmental measurements.
- Invalid incident-report payloads.
- Unauthorized database access attempts.
- Duplicate or contradictory community reports.
- Backend unavailability.
- Frontend behaviour when real-time updates fail.

These scenarios help assess both normal operation and failure handling.

---

## 🌍 Business and Sustainability Model

FloodSiren is designed around a public-safety-first approach.

### 1. Free Public Safety Access

**Target Users:** Residents in flood-prone communities.

Potential free services include basic flood-risk information, accessible warnings, and community reporting.

The long-term goal is to avoid making essential safety information dependent on a user's ability to pay.

### 2. Municipalities and Disaster-Management Services

**Potential Model:** Business-to-government (B2G) subscriptions or service agreements.

Potential paid capabilities include:

- Operational hazard-monitoring dashboards.
- Community incident-management tools.
- Geographic risk summaries.
- Reporting and response coordination.
- Integration with existing disaster-management systems.

### 3. Insurance and Enterprise Services

**Potential Model:** Business-to-business (B2B) data services.

Subject to appropriate consent, licensing, privacy safeguards, data quality, and validation, aggregated environmental insights could support risk-management and resilience planning for insurers, agricultural businesses, and other enterprises.

### Sustainability Considerations

A viable long-term service would require reliable data sources, hosting, security maintenance, telecom integration, community partnerships, and ongoing operational support.

Any commercial use of data must preserve the platform's public-safety mission and avoid exposing sensitive personal or location information.

---

## 🗺️ Limitations and Future Roadmap

FloodSiren is a hackathon-stage concept and prototype. Its operational capabilities depend on the features implemented, data sources connected, and services successfully deployed.

Potential future development includes:

- Integration with verified weather and hydrological data sources.
- Local calibration and validation of risk models.
- Testing against historical flood events.
- Operational SMS delivery through a messaging provider.
- Integration with an authorized USSD gateway.
- Offline-friendly interfaces and low-bandwidth optimization.
- Geographic risk mapping and improved location coverage.
- Verification workflows for community reports.
- Partnerships with municipalities and disaster-management authorities.
- Monitoring, reliability testing, and production incident response.

The roadmap prioritizes reliable risk communication, transparent uncertainty, and accessibility alongside technical sophistication.

---

## 🤝 Contributing

FloodSiren is being developed collaboratively by Team FloodSiren for the FNB App of the Year Hackathon 2026.

To contribute:

1. Fork or clone the repository.
2. Create a feature branch.
3. Make focused changes and test them.
4. Document relevant configuration changes.
5. Submit a pull request for review.

Please do not commit credentials, personal information, or unverified claims about production functionality.

---

## 👥 Team FloodSiren

**Ayanda Sibanda** — Backend, Database & Predictive Data Lead  
**Selemani Ecasa** — Frontend, UI/UX & Product Lead

Built for the **FNB App of the Year Hackathon 2026**.

*FloodSiren: Clearer warnings. Safer decisions. More resilient communities.*
