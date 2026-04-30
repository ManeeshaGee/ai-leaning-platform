# 🎓 AI-Powered Personalized Learning Platform

> A final-year undergraduate Software Engineering project — a cloud-native, MERN-based e-learning platform that adapts content, quizzes, and learning paths in real time based on each learner's performance and knowledge gaps.

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat&logo=mongodb&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat&logo=express&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-FF9900?style=flat&logo=amazonaws&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)

---# 🎓 AI-Driven Personalized Learning Platform

> A final-year undergraduate Software Engineering project — a cloud-native e-learning platform built with Next.js, Node.js, Express, and MongoDB that adapts content, quizzes, and learning paths in real time based on each learner's performance and knowledge gaps.

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat&logo=next.js&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat&logo=mongodb&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat&logo=express&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-FF9900?style=flat&logo=amazonaws&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [System Architecture](#system-architecture)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Core AI Features](#core-ai-features)
  - [Knowledge Tracing (DKT)](#1-knowledge-tracing-with-dkt)
  - [LLM Question Generator](#2-llm-powered-question-generator)
  - [Recommendation Engine](#3-recommendation-engine)
  - [RAG-Based AI Tutor](#4-rag-based-ai-tutor)
  - [Real-Time Progress](#5-real-time-progress-with-socketio)
- [Cloud Infrastructure](#cloud-infrastructure)
- [Build Phases](#build-phases)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Contributing](#contributing)

---

## Overview

This platform goes far beyond CRUD — it uses AI to personalize each student's learning journey. The system continuously tracks mastery levels per concept using Deep Knowledge Tracing (DKT), generates adaptive quizzes with LLMs, recommends the next best module, and provides a context-aware AI tutor powered by Retrieval-Augmented Generation (RAG).

**This is not a static course website.** Every student gets a unique, evolving learning path driven by real-time AI inference.

### Why Next.js?

Next.js 14 with the App Router gives this platform meaningful advantages over a plain React SPA:

- **Server Components** — Course listings, module details, and the dashboard shell are server-rendered, so first load is fast and SEO-friendly with zero client-side JS overhead for static parts
- **SSR / ISR** — Course catalogue pages are Incrementally Static Regenerated, meaning content is fresh without hitting the backend on every request
- **API Routes** — Lightweight Next.js API routes handle session checks and light data fetching, keeping the Express backend focused on heavy business logic and AI calls
- **Streaming** — The AI tutor response streams token-by-token to the UI using Next.js streaming + React Suspense
- **Built-in Image Optimisation** — Course thumbnails and instructor avatars are automatically resized and served via Next.js Image, reducing CloudFront bandwidth costs

---

## Key Features

- 🧠 **Deep Knowledge Tracing (DKT)** — LSTM-based model that predicts mastery probability per concept from interaction history
- ✍️ **LLM Question Generation** — Dynamically generated quiz questions at the right difficulty level using the Anthropic API
- 🗺️ **Adaptive Learning Paths** — Recommends the next module based on concept gaps and prerequisite mastery
- 🤖 **RAG AI Tutor** — Students ask questions and get answers grounded in actual course content via vector search
- ⚡ **Real-Time Dashboard** — Live mastery score updates and next-step recommendations via Socket.io
- ☁️ **Cloud-Native** — CDN-delivered content, SageMaker ML hosting, S3 storage, and Redis caching

---

## System Architecture

```
┌─────────────────────────────────────────────────────┐
│             Frontend — Next.js 14 (App Router)       │
│  Dashboard · Quiz UI · Learning map · AI Chat Tutor  │
│  SSR pages · API Routes · Server Components          │
└───────────────────┬─────────────────────────────────┘
                    │ REST + WebSocket
         ┌──────────┴──────────┐
         │                     │
┌────────▼────────┐   ┌────────▼────────┐
│  API Gateway    │   │ WebSocket Server │
│ Express + JWT   │   │   Socket.io      │
└────────┬────────┘   └────────┬────────┘
         │                     │
┌────────▼─────────────────────▼────────┐
│           Backend Services (Node.js)   │
│  User · Content · Quiz · Analytics    │
└────────────────────┬──────────────────┘
                     │
┌────────────────────▼──────────────────┐
│              AI Layer                  │
│  DKT Model · LLM Generator            │
│  Recommender · RAG Tutor              │
└────────────────────┬──────────────────┘
                     │
┌────────────────────▼──────────────────┐
│           Data & Storage               │
│  MongoDB Atlas · Redis · Pinecone · S3 │
└────────────────────┬──────────────────┘
                     │
┌────────────────────▼──────────────────┐
│       Cloud Infrastructure (AWS)       │
│  EC2 · CloudFront · SageMaker · SQS   │
└───────────────────────────────────────┘
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | Next.js 14 (App Router), TailwindCSS, Recharts, Socket.io-client, Server Components |
| **Backend** | Node.js, Express.js, Mongoose, BullMQ |
| **AI / ML** | Anthropic API, Python FastAPI, PyTorch (DKT), LangChain |
| **Databases** | MongoDB Atlas, Redis (Upstash), Pinecone (vector DB) |
| **Cloud** | AWS S3, CloudFront CDN, SageMaker, SQS + Lambda |
| **DevOps** | GitHub Actions, Docker, AWS EC2 |

---

## Project Structure

```
ai-learning-platform/
├── client/                        # Next.js 14 frontend (App Router)
│   ├── app/
│   │   ├── layout.tsx             # Root layout (fonts, providers)
│   │   ├── page.tsx               # Landing / home page (SSR)
│   │   ├── (auth)/
│   │   │   ├── login/page.tsx
│   │   │   └── register/page.tsx
│   │   ├── dashboard/
│   │   │   └── page.tsx           # Mastery charts, progress map (SSR)
│   │   ├── courses/
│   │   │   ├── page.tsx           # Course listing (SSR + ISR)
│   │   │   └── [courseId]/
│   │   │       ├── page.tsx       # Course detail (dynamic SSR)
│   │   │       └── quiz/page.tsx  # Adaptive quiz (Client Component)
│   │   └── tutor/
│   │       └── page.tsx           # AI chat tutor (Client Component)
│   ├── components/
│   │   ├── Dashboard/             # Mastery charts, progress map
│   │   ├── Quiz/                  # Adaptive quiz UI
│   │   ├── Tutor/                 # AI chat interface
│   │   └── LearningPath/          # Visual module map
│   ├── hooks/
│   │   ├── useSocket.ts           # Real-time updates (client-side)
│   │   └── useMastery.ts          # Mastery score state
│   ├── lib/
│   │   └── api.ts                 # Fetch helpers for backend API
│   └── next.config.js
│
├── server/                        # Node.js backend
│   ├── services/
│   │   ├── user/                  # Auth, profiles, roles
│   │   ├── content/               # Modules, lessons, videos
│   │   ├── quiz/                  # Generation + grading
│   │   └── analytics/             # Event tracking, logs
│   ├── ai/
│   │   ├── dkt/                   # DKT model client (calls Python service)
│   │   ├── llm/                   # LLM question generator
│   │   ├── recommender/           # Learning path logic
│   │   └── rag/                   # Vector search + tutor
│   ├── jobs/                      # BullMQ background workers
│   ├── socket/                    # Socket.io event handlers
│   └── middleware/                # Auth, rate limiting, logging
│
├── ai-service/                    # Python FastAPI microservice
│   ├── models/
│   │   └── dkt_model.py           # PyTorch LSTM model
│   ├── routes/
│   │   ├── predict.py             # /dkt/predict endpoint
│   │   └── train.py               # /dkt/train endpoint
│   └── main.py
│
└── infra/                         # IaC & DevOps
    ├── docker-compose.yml
    ├── .github/workflows/
    └── terraform/                 # AWS resource definitions
```

---

## Core AI Features

### 1. Knowledge Tracing with DKT

The engine that tracks how well a student knows each concept over time. Every answer event is recorded and fed into an LSTM-based Deep Knowledge Tracing model that predicts the current mastery probability for every concept.

**Interaction Schema (MongoDB):**

```js
// models/UserInteraction.js
const interactionSchema = new mongoose.Schema({
  userId:       { type: ObjectId, ref: 'User', required: true },
  conceptId:    { type: ObjectId, ref: 'Concept', required: true },
  questionId:   { type: ObjectId, ref: 'Question', required: true },
  correct:      Boolean,
  difficulty:   { type: String, enum: ['beginner', 'intermediate', 'advanced'] },
  timeSpentMs:  Number,
  timestamp:    { type: Date, default: Date.now }
});
```

**Calling the DKT Microservice:**

```js
// server/ai/dkt/index.js
const getMasteryScores = async (userId) => {
  const history = await UserInteraction.find({ userId })
    .sort({ timestamp: -1 })
    .limit(50)
    .lean();

  const { data } = await axios.post(
    `${process.env.DKT_SERVICE_URL}/predict`,
    { userId, history }
  );

  // Returns: { "algebra-basics": 0.85, "quadratics": 0.42, ... }
  return data.mastery;
};
```

**Python DKT Service (FastAPI):**

```python
# ai-service/routes/predict.py
@app.post("/dkt/predict")
async def predict_mastery(payload: PredictRequest):
    sequences = encode_interactions(payload.history)
    with torch.no_grad():
        mastery_probs = model(sequences)  # LSTM forward pass
    return {
        "mastery": {
            concept: float(prob)
            for concept, prob in zip(payload.concept_ids, mastery_probs)
        }
    }
```

---

### 2. LLM-Powered Question Generator

Instead of a static question bank, fresh questions are generated dynamically at the right difficulty based on the student's current mastery score.

```js
// server/ai/llm/questionGenerator.js
const generateQuestion = async (conceptId, masteryScore) => {
  const difficulty = masteryScore < 0.4  ? 'beginner'
                   : masteryScore < 0.75 ? 'intermediate'
                   :                       'advanced';

  const concept = await Concept.findById(conceptId);

  const prompt = `
    You are an expert tutor. Generate a ${difficulty}-level question about:
    "${concept.name}" — ${concept.description}

    Respond ONLY in this JSON format:
    {
      "question": "...",
      "options": ["A", "B", "C", "D"],
      "correctIndex": 0,
      "explanation": "..."
    }
  `;

  const response = await anthropic.messages.create({
    model: "claude-opus-4-5",
    max_tokens: 600,
    messages: [{ role: "user", content: prompt }]
  });

  return JSON.parse(response.content[0].text);
};
```

---

### 3. Recommendation Engine

After each quiz session, the system selects the next best learning module based on mastery gaps, prerequisite completion, and whether the module is a core requirement.

```js
// server/ai/recommender/index.js
const getNextModule = async (userId) => {
  const masteryMap    = await getMasteryScores(userId);
  const completedIds  = await getCompletedModules(userId);
  const allModules    = await Module.find({ _id: { $nin: completedIds } })
                                    .populate('prerequisites');

  const scored = allModules.map(module => {
    const prereqMet = module.prerequisites.every(
      p => (masteryMap[p.conceptId] || 0) >= 0.6
    );
    const conceptGap = 1 - (masteryMap[module.conceptId] || 0);
    const urgency    = module.isCore ? 1.5 : 1.0;

    return {
      module,
      score: prereqMet ? conceptGap * urgency : -1
    };
  });

  return scored
    .filter(s => s.score > 0)
    .sort((a, b) => b.score - a.score)
    .slice(0, 3)
    .map(s => s.module);
};
```

---

### 4. RAG-Based AI Tutor

Students can ask questions in natural language and receive answers grounded in actual course content — not hallucinated responses — using vector search over embedded course material.

```js
// server/ai/rag/tutor.js
const answerQuestion = async (userQuestion, courseId) => {
  // 1. Embed the student's question
  const embedding = await openai.embeddings.create({
    input: userQuestion,
    model: "text-embedding-3-small"
  });

  // 2. Retrieve relevant course content chunks from Pinecone
  const results = await pinecone.index('course-content').query({
    vector: embedding.data[0].embedding,
    topK: 5,
    filter: { courseId }
  });

  const context = results.matches
    .map(r => r.metadata.text)
    .join('\n\n');

  // 3. Generate a grounded answer using retrieved context
  const response = await anthropic.messages.create({
    model: "claude-sonnet-4-6",
    max_tokens: 800,
    system: `You are a helpful tutor. Answer ONLY using the provided context.
             If the answer is not in the context, say so honestly.`,
    messages: [{
      role: "user",
      content: `Context:\n${context}\n\nQuestion: ${userQuestion}`
    }]
  });

  return response.content[0].text;
};
```

**Ingesting course content into Pinecone:**

```js
// server/ai/rag/ingest.js
const ingestCourseContent = async (module) => {
  const chunks = splitIntoChunks(module.content, 500); // 500 token chunks

  const embeddings = await Promise.all(
    chunks.map(chunk =>
      openai.embeddings.create({ input: chunk, model: "text-embedding-3-small" })
    )
  );

  await pinecone.index('course-content').upsert(
    chunks.map((chunk, i) => ({
      id: `${module._id}-chunk-${i}`,
      values: embeddings[i].data[0].embedding,
      metadata: { text: chunk, courseId: module.courseId, moduleId: module._id }
    }))
  );
};
```

---

### 5. Real-Time Progress with Socket.io

When a student submits an answer, mastery scores and module recommendations update instantly on the dashboard without a page reload.

```js
// server/socket/index.js
io.on('connection', (socket) => {

  socket.on('answer:submit', async ({ userId, questionId, answer }) => {
    const result      = await gradeAnswer(questionId, answer);
    await saveInteraction(userId, result);

    const newMastery  = await getMasteryScores(userId);   // DKT inference
    const nextModules = await getNextModule(userId);       // Recommender

    // Push live update to the student's session
    socket.emit('progress:updated', {
      mastery:     newMastery,
      nextModules,
      streakCount: await getStreak(userId)
    });
  });

  socket.on('tutor:ask', async ({ userId, question, courseId }) => {
    const answer = await answerQuestion(question, courseId);
    socket.emit('tutor:reply', { answer });
  });

});
```

---

## Cloud Infrastructure

| Service | Purpose | Tool |
|---|---|---|
| **Compute** | Host Node.js API | AWS EC2 / Render |
| **ML Hosting** | Serve DKT model endpoint | AWS SageMaker |
| **CDN** | Deliver videos and PDFs fast globally | AWS CloudFront |
| **Object Storage** | Store course content files | AWS S3 |
| **Primary DB** | User data, interactions, modules | MongoDB Atlas |
| **Cache** | Sessions and real-time mastery scores | Redis (Upstash / ElastiCache) |
| **Vector DB** | RAG embeddings for AI tutor | Pinecone (free tier) |
| **Job Queue** | Async model re-training, email jobs | AWS SQS + Lambda |
| **CI/CD** | Auto-deploy on push to main | GitHub Actions |
| **Monitoring** | Logs, alerts, performance metrics | AWS CloudWatch |

---

## Build Phases

| Phase | Weeks | Goals |
|---|---|---|
| **Phase 1 — Foundation** | 1–3 | Auth, course CRUD, MongoDB schema design, basic quiz with static questions |
| **Phase 2 — LLM Integration** | 4–6 | LLM question generation, answer grading, interaction event logging |
| **Phase 3 — Adaptive AI** | 7–9 | DKT model integration, mastery scoring, recommendation engine |
| **Phase 4 — Real-Time + RAG** | 10–12 | RAG AI tutor, Socket.io live dashboard, Redis caching |
| **Phase 5 — Cloud Deploy** | 13–14 | CDN setup, SageMaker hosting, S3 storage, CI/CD pipeline, monitoring |

---

## Getting Started

### Prerequisites

- Node.js v18+
- Python 3.10+
- MongoDB Atlas account
- Redis instance (local or Upstash)
- Pinecone account (free tier)
- Anthropic API key
- AWS account

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/ai-learning-platform.git
cd ai-learning-platform

# Install backend dependencies
cd server && npm install

# Install frontend dependencies (Next.js)
cd ../client && npm install

# Set up the Python AI service
cd ../ai-service
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
```

### Running Locally

```bash
# Terminal 1 — Start MongoDB (if local)
mongod

# Terminal 2 — Start Redis (if local)
redis-server

# Terminal 3 — Start Python DKT service
cd ai-service && uvicorn main:app --port 8000 --reload

# Terminal 4 — Start Node.js backend
cd server && npm run dev

# Terminal 5 — Start Next.js frontend
cd client && npm run dev        # Runs on http://localhost:3000
```

### Using Docker Compose

```bash
docker-compose up --build
```

---

## Environment Variables

**`/server/.env`**

```env
# App
PORT=5000
NODE_ENV=development

# MongoDB
MONGO_URI=mongodb+srv://<user>:<pass>@cluster.mongodb.net/ai-learning

# JWT
JWT_SECRET=your_jwt_secret_here
JWT_EXPIRES_IN=7d

# Redis
REDIS_URL=redis://localhost:6379

# AI Services
ANTHROPIC_API_KEY=sk-ant-...
OPENAI_API_KEY=sk-...
DKT_SERVICE_URL=http://localhost:8000

# Pinecone
PINECONE_API_KEY=your_pinecone_key
PINECONE_ENVIRONMENT=us-east-1-aws

# AWS
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...
AWS_REGION=us-east-1
S3_BUCKET_NAME=ai-learning-content
CLOUDFRONT_DOMAIN=https://your-distribution.cloudfront.net
```

**`/client/.env.local`**

```env
# Backend API (used by Next.js server components + API routes)
NEXT_PUBLIC_API_URL=http://localhost:5000
NEXT_PUBLIC_SOCKET_URL=http://localhost:5000

# Next.js Auth
NEXTAUTH_SECRET=your_nextauth_secret
NEXTAUTH_URL=http://localhost:3000
```

---

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m 'Add my feature'`
4. Push to the branch: `git push origin feature/my-feature`
5. Open a Pull Request

---

## License

This project is built as a final year undergraduate project for academic purposes.

---

> Built with ❤️ using Next.js + Node.js + MongoDB + AI + Cloud

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [System Architecture](#system-architecture)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Core AI Features](#core-ai-features)
  - [Knowledge Tracing (DKT)](#1-knowledge-tracing-with-dkt)
  - [LLM Question Generator](#2-llm-powered-question-generator)
  - [Recommendation Engine](#3-recommendation-engine)
  - [RAG-Based AI Tutor](#4-rag-based-ai-tutor)
  - [Real-Time Progress](#5-real-time-progress-with-socketio)
- [Cloud Infrastructure](#cloud-infrastructure)
- [Build Phases](#build-phases)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Contributing](#contributing)

---

## Overview

This platform goes far beyond CRUD — it uses AI to personalize each student's learning journey. The system continuously tracks mastery levels per concept using Deep Knowledge Tracing (DKT), generates adaptive quizzes with LLMs, recommends the next best module, and provides a context-aware AI tutor powered by Retrieval-Augmented Generation (RAG).

**This is not a static course website.** Every student gets a unique, evolving learning path driven by real-time AI inference.

---

## Key Features

- 🧠 **Deep Knowledge Tracing (DKT)** — LSTM-based model that predicts mastery probability per concept from interaction history
- ✍️ **LLM Question Generation** — Dynamically generated quiz questions at the right difficulty level using the Anthropic API
- 🗺️ **Adaptive Learning Paths** — Recommends the next module based on concept gaps and prerequisite mastery
- 🤖 **RAG AI Tutor** — Students ask questions and get answers grounded in actual course content via vector search
- ⚡ **Real-Time Dashboard** — Live mastery score updates and next-step recommendations via Socket.io
- ☁️ **Cloud-Native** — CDN-delivered content, SageMaker ML hosting, S3 storage, and Redis caching

---

## System Architecture

```
┌─────────────────────────────────────────────────────┐
│              Frontend — React.js (Vite)             │
│  Dashboard · Quiz UI · Learning map · AI Chat Tutor │
└───────────────────┬─────────────────────────────────┘
                    │ REST + WebSocket
         ┌──────────┴──────────┐
         │                     │
┌────────▼────────┐   ┌────────▼────────┐
│  API Gateway    │   │ WebSocket Server │
│ Express + JWT   │   │   Socket.io      │
└────────┬────────┘   └────────┬────────┘
         │                     │
┌────────▼─────────────────────▼────────┐
│           Backend Services (Node.js)   │
│  User · Content · Quiz · Analytics    │
└────────────────────┬──────────────────┘
                     │
┌────────────────────▼──────────────────┐
│              AI Layer                  │
│  DKT Model · LLM Generator            │
│  Recommender · RAG Tutor              │
└────────────────────┬──────────────────┘
                     │
┌────────────────────▼──────────────────┐
│           Data & Storage               │
│  MongoDB Atlas · Redis · Pinecone · S3 │
└────────────────────┬──────────────────┘
                     │
┌────────────────────▼──────────────────┐
│       Cloud Infrastructure (AWS)       │
│  EC2 · CloudFront · SageMaker · SQS   │
└───────────────────────────────────────┘
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | React.js (Vite), TailwindCSS, Recharts, Socket.io-client |
| **Backend** | Node.js, Express.js, Mongoose, BullMQ |
| **AI / ML** | Anthropic API, Python FastAPI, PyTorch (DKT), LangChain |
| **Databases** | MongoDB Atlas, Redis (Upstash), Pinecone (vector DB) |
| **Cloud** | AWS S3, CloudFront CDN, SageMaker, SQS + Lambda |
| **DevOps** | GitHub Actions, Docker, AWS EC2 |

---

## Project Structure

```
ai-learning-platform/
├── client/                        # React frontend
│   ├── src/
│   │   ├── components/
│   │   │   ├── Dashboard/         # Mastery charts, progress map
│   │   │   ├── Quiz/              # Adaptive quiz UI
│   │   │   ├── Tutor/             # AI chat interface
│   │   │   └── LearningPath/      # Visual module map
│   │   ├── hooks/
│   │   │   ├── useSocket.js       # Real-time updates
│   │   │   └── useMastery.js      # Mastery score state
│   │   └── pages/
│
├── server/                        # Node.js backend
│   ├── services/
│   │   ├── user/                  # Auth, profiles, roles
│   │   ├── content/               # Modules, lessons, videos
│   │   ├── quiz/                  # Generation + grading
│   │   └── analytics/             # Event tracking, logs
│   ├── ai/
│   │   ├── dkt/                   # DKT model client (calls Python service)
│   │   ├── llm/                   # LLM question generator
│   │   ├── recommender/           # Learning path logic
│   │   └── rag/                   # Vector search + tutor
│   ├── jobs/                      # BullMQ background workers
│   ├── socket/                    # Socket.io event handlers
│   └── middleware/                # Auth, rate limiting, logging
│
├── ai-service/                    # Python FastAPI microservice
│   ├── models/
│   │   └── dkt_model.py           # PyTorch LSTM model
│   ├── routes/
│   │   ├── predict.py             # /dkt/predict endpoint
│   │   └── train.py               # /dkt/train endpoint
│   └── main.py
│
└── infra/                         # IaC & DevOps
    ├── docker-compose.yml
    ├── .github/workflows/
    └── terraform/                 # AWS resource definitions
```

---

## Core AI Features

### 1. Knowledge Tracing with DKT

The engine that tracks how well a student knows each concept over time. Every answer event is recorded and fed into an LSTM-based Deep Knowledge Tracing model that predicts the current mastery probability for every concept.

**Interaction Schema (MongoDB):**

```js
// models/UserInteraction.js
const interactionSchema = new mongoose.Schema({
  userId:       { type: ObjectId, ref: 'User', required: true },
  conceptId:    { type: ObjectId, ref: 'Concept', required: true },
  questionId:   { type: ObjectId, ref: 'Question', required: true },
  correct:      Boolean,
  difficulty:   { type: String, enum: ['beginner', 'intermediate', 'advanced'] },
  timeSpentMs:  Number,
  timestamp:    { type: Date, default: Date.now }
});
```

**Calling the DKT Microservice:**

```js
// server/ai/dkt/index.js
const getMasteryScores = async (userId) => {
  const history = await UserInteraction.find({ userId })
    .sort({ timestamp: -1 })
    .limit(50)
    .lean();

  const { data } = await axios.post(
    `${process.env.DKT_SERVICE_URL}/predict`,
    { userId, history }
  );

  // Returns: { "algebra-basics": 0.85, "quadratics": 0.42, ... }
  return data.mastery;
};
```

**Python DKT Service (FastAPI):**

```python
# ai-service/routes/predict.py
@app.post("/dkt/predict")
async def predict_mastery(payload: PredictRequest):
    sequences = encode_interactions(payload.history)
    with torch.no_grad():
        mastery_probs = model(sequences)  # LSTM forward pass
    return {
        "mastery": {
            concept: float(prob)
            for concept, prob in zip(payload.concept_ids, mastery_probs)
        }
    }
```

---

### 2. LLM-Powered Question Generator

Instead of a static question bank, fresh questions are generated dynamically at the right difficulty based on the student's current mastery score.

```js
// server/ai/llm/questionGenerator.js
const generateQuestion = async (conceptId, masteryScore) => {
  const difficulty = masteryScore < 0.4  ? 'beginner'
                   : masteryScore < 0.75 ? 'intermediate'
                   :                       'advanced';

  const concept = await Concept.findById(conceptId);

  const prompt = `
    You are an expert tutor. Generate a ${difficulty}-level question about:
    "${concept.name}" — ${concept.description}

    Respond ONLY in this JSON format:
    {
      "question": "...",
      "options": ["A", "B", "C", "D"],
      "correctIndex": 0,
      "explanation": "..."
    }
  `;

  const response = await anthropic.messages.create({
    model: "claude-opus-4-5",
    max_tokens: 600,
    messages: [{ role: "user", content: prompt }]
  });

  return JSON.parse(response.content[0].text);
};
```

---

### 3. Recommendation Engine

After each quiz session, the system selects the next best learning module based on mastery gaps, prerequisite completion, and whether the module is a core requirement.

```js
// server/ai/recommender/index.js
const getNextModule = async (userId) => {
  const masteryMap    = await getMasteryScores(userId);
  const completedIds  = await getCompletedModules(userId);
  const allModules    = await Module.find({ _id: { $nin: completedIds } })
                                    .populate('prerequisites');

  const scored = allModules.map(module => {
    const prereqMet = module.prerequisites.every(
      p => (masteryMap[p.conceptId] || 0) >= 0.6
    );
    const conceptGap = 1 - (masteryMap[module.conceptId] || 0);
    const urgency    = module.isCore ? 1.5 : 1.0;

    return {
      module,
      score: prereqMet ? conceptGap * urgency : -1
    };
  });

  return scored
    .filter(s => s.score > 0)
    .sort((a, b) => b.score - a.score)
    .slice(0, 3)
    .map(s => s.module);
};
```

---

### 4. RAG-Based AI Tutor

Students can ask questions in natural language and receive answers grounded in actual course content — not hallucinated responses — using vector search over embedded course material.

```js
// server/ai/rag/tutor.js
const answerQuestion = async (userQuestion, courseId) => {
  // 1. Embed the student's question
  const embedding = await openai.embeddings.create({
    input: userQuestion,
    model: "text-embedding-3-small"
  });

  // 2. Retrieve relevant course content chunks from Pinecone
  const results = await pinecone.index('course-content').query({
    vector: embedding.data[0].embedding,
    topK: 5,
    filter: { courseId }
  });

  const context = results.matches
    .map(r => r.metadata.text)
    .join('\n\n');

  // 3. Generate a grounded answer using retrieved context
  const response = await anthropic.messages.create({
    model: "claude-sonnet-4-6",
    max_tokens: 800,
    system: `You are a helpful tutor. Answer ONLY using the provided context.
             If the answer is not in the context, say so honestly.`,
    messages: [{
      role: "user",
      content: `Context:\n${context}\n\nQuestion: ${userQuestion}`
    }]
  });

  return response.content[0].text;
};
```

**Ingesting course content into Pinecone:**

```js
// server/ai/rag/ingest.js
const ingestCourseContent = async (module) => {
  const chunks = splitIntoChunks(module.content, 500); // 500 token chunks

  const embeddings = await Promise.all(
    chunks.map(chunk =>
      openai.embeddings.create({ input: chunk, model: "text-embedding-3-small" })
    )
  );

  await pinecone.index('course-content').upsert(
    chunks.map((chunk, i) => ({
      id: `${module._id}-chunk-${i}`,
      values: embeddings[i].data[0].embedding,
      metadata: { text: chunk, courseId: module.courseId, moduleId: module._id }
    }))
  );
};
```

---

### 5. Real-Time Progress with Socket.io

When a student submits an answer, mastery scores and module recommendations update instantly on the dashboard without a page reload.

```js
// server/socket/index.js
io.on('connection', (socket) => {

  socket.on('answer:submit', async ({ userId, questionId, answer }) => {
    // Grade, save, and trigger AI pipeline
    const result      = await gradeAnswer(questionId, answer);
    await saveInteraction(userId, result);

    const newMastery  = await getMasteryScores(userId);   // DKT inference
    const nextModules = await getNextModule(userId);       // Recommender

    // Push live update to the student's session
    socket.emit('progress:updated', {
      mastery:     newMastery,
      nextModules,
      streakCount: await getStreak(userId)
    });
  });

  socket.on('tutor:ask', async ({ userId, question, courseId }) => {
    const answer = await answerQuestion(question, courseId);
    socket.emit('tutor:reply', { answer });
  });

});
```

---

## Cloud Infrastructure

| Service | Purpose | Tool |
|---|---|---|
| **Compute** | Host Node.js API | AWS EC2 / Render |
| **ML Hosting** | Serve DKT model endpoint | AWS SageMaker |
| **CDN** | Deliver videos and PDFs fast globally | AWS CloudFront |
| **Object Storage** | Store course content files | AWS S3 |
| **Primary DB** | User data, interactions, modules | MongoDB Atlas |
| **Cache** | Sessions and real-time mastery scores | Redis (Upstash / ElastiCache) |
| **Vector DB** | RAG embeddings for AI tutor | Pinecone (free tier) |
| **Job Queue** | Async model re-training, email jobs | AWS SQS + Lambda |
| **CI/CD** | Auto-deploy on push to main | GitHub Actions |
| **Monitoring** | Logs, alerts, performance metrics | AWS CloudWatch |

---

## Build Phases

| Phase | Weeks | Goals |
|---|---|---|
| **Phase 1 — Foundation** | 1–3 | Auth, course CRUD, MongoDB schema design, basic quiz with static questions |
| **Phase 2 — LLM Integration** | 4–6 | LLM question generation, answer grading, interaction event logging |
| **Phase 3 — Adaptive AI** | 7–9 | DKT model integration, mastery scoring, recommendation engine |
| **Phase 4 — Real-Time + RAG** | 10–12 | RAG AI tutor, Socket.io live dashboard, Redis caching |
| **Phase 5 — Cloud Deploy** | 13–14 | CDN setup, SageMaker hosting, S3 storage, CI/CD pipeline, monitoring |

---

## Getting Started

### Prerequisites

- Node.js v18+
- Python 3.10+
- MongoDB Atlas account
- Redis instance (local or Upstash)
- Pinecone account (free tier)
- Anthropic API key
- AWS account

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/ai-learning-platform.git
cd ai-learning-platform

# Install backend dependencies
cd server && npm install

# Install frontend dependencies
cd ../client && npm install

# Set up the Python AI service
cd ../ai-service
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
```

### Running Locally

```bash
# Terminal 1 — Start MongoDB (if local)
mongod

# Terminal 2 — Start Redis (if local)
redis-server

# Terminal 3 — Start Python DKT service
cd ai-service && uvicorn main:app --port 8000 --reload

# Terminal 4 — Start Node.js backend
cd server && npm run dev

# Terminal 5 — Start React frontend
cd client && npm run dev
```

### Using Docker Compose

```bash
docker-compose up --build
```

---

## Environment Variables

Create a `.env` file in the `/server` directory:

```env
# App
PORT=5000
NODE_ENV=development

# MongoDB
MONGO_URI=mongodb+srv://<user>:<pass>@cluster.mongodb.net/ai-learning

# JWT
JWT_SECRET=your_jwt_secret_here
JWT_EXPIRES_IN=7d

# Redis
REDIS_URL=redis://localhost:6379

# AI Services
ANTHROPIC_API_KEY=sk-ant-...
OPENAI_API_KEY=sk-...
DKT_SERVICE_URL=http://localhost:8000

# Pinecone
PINECONE_API_KEY=your_pinecone_key
PINECONE_ENVIRONMENT=us-east-1-aws

# AWS
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...
AWS_REGION=us-east-1
S3_BUCKET_NAME=ai-learning-content
CLOUDFRONT_DOMAIN=https://your-distribution.cloudfront.net
```

---

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m 'Add my feature'`
4. Push to the branch: `git push origin feature/my-feature`
5. Open a Pull Request

---

## License

This project is built as a final year undergraduate project for academic purposes.

---

> Built with ❤️ using MERN + AI + Cloud
