# EcoLoop AI — Circular Waste Intelligence Platform

> “WASTE IS A RESOURCE OUT OF PLACE.”  
> **Identify it. Collect it. Route it. Recover it.**

EcoLoop AI is an AI-powered municipal waste segregation, doorstep collection routing, and circular recycling distribution platform designed for Indian urban local bodies (ULBs), compliant with the **Solid Waste Management Rules 2016 (SWM 2016)** and Central Pollution Control Board (CPCB) standards.

---

## 1. Visual & Architectural Identity

EcoLoop AI employs a **Brutalist Eco-Tech** design language combining:
- Contemporary web brutalism and neo-brutalist editorial typography (Space Grotesk & Archivo Black display, JetBrains Mono data coordinates, Inter body).
- Raw industrial recycling aesthetic: utility markings, bold grids, oversized numbers, square corners, and hard offset drop shadows (`4px 4px 0px #171914`).
- Colour Palette:
  - **Recycled Paper Ivory**: `#F2F0E6` (Warm foundation)
  - **Deep Ink Black**: `#171914` (High-contrast structural framing)
  - **Electric Acid Lime**: `#C7FF38` (Primary call to action & verified highlights)
  - **Recycled Orange**: `#FF6338` (Hazard alerts & secondary badges)
  - **Muted Concrete Grey**: `#B9B9AE` (Auxiliary telemetry)

---

## 2. Key Modules & Routes

1. **System Overview (`/`)**: High-impact editorial landing page with live municipal recovery statistics, 5-stage circular lifecycle (01 IDENTIFY → 02 SEGREGATE → 03 COLLECT → 04 DISTRIBUTE → 05 RECOVER), interactive material database, and multi-stakeholder ecosystem.
2. **AI Waste Scanner (`/scan`)**: Camera-first multimodal packaging inspector. Supports live web camera streaming, photo file uploads, and 6 one-click test packaging presets. Powered by Gemini 3.8 Flash multimodal vision with explicit confidence reporting and demo disclosures.
3. **Citizen Eco-Credit Hub (`/dashboard`)**: Resident portal displaying Segregation Accuracy Score (out of 100), redeemable EcoPoints balance, active pickup tracking stepper, and localized municipal ward selector (BBMP, MCD, BMC, PMC).
4. **Doorstep Logistics (`/pickups`)**: 5-step pickup booking system with category selection, estimated weight (kg), address picker, date/time-slots, and OTP-secured handover.
5. **Recycler Marketplace (`/recyclers`)**: Material-exchange marketplace connecting municipal Material Recovery Facilities (MRFs) with CPCB-authorized industrial recyclers, including CPCB Form-6 manifest hashes and batch transfer requests.
6. **Safai Mitra Field PWA (`/collector`)**: High-contrast outdoor-optimized mobile interface for waste collectors. Record scale weight, verify customer handover OTP, capture S3 scale proof, and report cross-contamination.
7. **Municipal ULB Command Center (`/admin`)**: Administrative intelligence dashboard displaying gross weight collected vs MRF accepted vs certified processed, Recharts mass-balance analytics, and searchable audit records.
8. **AWS Serverless Specification**: Interactive modal providing full AWS SAM template (`template.yaml`), DynamoDB single-table schema (PK/SK), Rekognition inference patterns, and CloudWatch audit metrics.

---

## 3. Technology Stack

### Frontend:
- **Framework**: React 19 with TypeScript
- **Styling**: Tailwind CSS v4 with bespoke brutalist hard-shadow design system
- **Icons**: Lucide Icons
- **Charts**: Recharts & Brutalist SVGs
- **Build Tool**: Vite 8 & TSX server

### Backend & AI Architecture:
- **Server Entrypoint**: Express on Node.js (`server.ts`) running Vite middleware in development
- **AI Inference Engine**: Google Gemini 3.8 Flash (`@google/genai`) multimodal vision API with graceful demo fallback
- **AWS Serverless Target Architecture**:
  - **Amazon Cognito**: User Pools & Groups (`citizen`, `safai_mitra`, `mrf_recycler`, `ulb_admin`)
  - **Amazon API Gateway**: HTTP API for REST endpoints
  - **AWS Lambda**: Python 3.12 business logic enforcing SWM state machine rules
  - **Amazon DynamoDB**: Single-table design with on-demand capacity
  - **Amazon S3**: Digital scale photograph storage and weighbridge certificates
  - **Amazon Rekognition Custom Labels**: Specialized municipal waste classification model
  - **Amazon CloudWatch**: End-to-end custody and contamination logging

---

## 4. Getting Started

### Prerequisites:
- Node.js 20+
- npm 10+

### Installation:
```bash
git clone <repo-url> ecoloop-ai
cd ecoloop-ai
npm install
```

### Running Locally:
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 5. Environment Configuration

Copy `.env.example` to `.env`:
```bash
cp .env.example .env
```

| Key | Description | Default |
|-----|-------------|---------|
| `GEMINI_API_KEY` | Gemini API Key for live AI waste vision inference | Injected at runtime |
| `APP_URL` | Application base hosting URL | Auto-injected |
| `AWS_REGION` | Target AWS Region | `ap-south-1` |
| `AWS_API_GATEWAY_URL` | Production AWS API Gateway HTTP URL | Optional |
| `USE_MOCK_STORAGE` | Enable client-side local storage demo engine | `true` |

---

## 6. AWS Deployment Instructions (SAM CLI)

To deploy the production AWS Serverless backend:

```bash
# 1. Install AWS SAM CLI
sam --version

# 2. Build SAM application
sam build

# 3. Deploy guided stack in ap-south-1 (Mumbai)
sam deploy --guided \
  --stack-name ecoloop-waste-intel-prod \
  --region ap-south-1 \
  --capabilities CAPABILITY_IAM
```

Once deployed, copy the generated `ApiEndpoint` URL into your `AWS_API_GATEWAY_URL` environment variable.

---

## 7. Compliance & Standards

- **CPCB SWM Rules 2016**: Adheres to 3-stream source segregation guidelines (Wet Biodegradable, Dry Recyclable, Domestic Hazardous).
- **PWM Rules 2024**: Full compliance with Extended Producer Responsibility (EPR) material category tracking (Category I Rigid Plastics, Category II Flexible Monolayer, Category III Multilayered).
- **DPDP Act 2023**: Citizen mobile numbers and exact geolocation coordinates are sanitized and access-controlled.

---

© 2026 EcoLoop AI Platform. Built for Indian Urban Local Bodies.
