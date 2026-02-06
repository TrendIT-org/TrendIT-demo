<p align="center">
  <img src="docs/images/trendit_logo.png" alt="TrendIT Logo" width="200" />
</p>

<h1 align="center">🎬 TrendIT AI Agent</h1>

<p align="center">
  <strong>AI-Powered Short-Form Video Feedback & Optimization Platform</strong>
</p>

<p align="center">
  <a href="#-features"><img src="https://img.shields.io/badge/Features-8_Step_Workflow-blue?style=for-the-badge" alt="Features" /></a>
  <a href="#-architecture"><img src="https://img.shields.io/badge/Architecture-LangGraph-green?style=for-the-badge" alt="Architecture" /></a>
  <a href="#-quick-start"><img src="https://img.shields.io/badge/Quick_Start-5_Minutes-orange?style=for-the-badge" alt="Quick Start" /></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.11+-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/FastAPI-0.100+-009688?style=flat-square&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/Next.js-14+-000000?style=flat-square&logo=next.js&logoColor=white" alt="Next.js" />
  <img src="https://img.shields.io/badge/TypeScript-5.0+-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/LangGraph-Stateful_Agent-4285F4?style=flat-square&logo=google&logoColor=white" alt="LangGraph" />
  <img src="https://img.shields.io/badge/MediaPipe-Pose_Analysis-FF6F00?style=flat-square&logo=google&logoColor=white" alt="MediaPipe" />
  <img src="https://img.shields.io/badge/Gemini-Multimodal_AI-8E75B2?style=flat-square&logo=google&logoColor=white" alt="Gemini" />
</p>

---


## 📖 Overview

**TrendIT AI Agent**는 틱톡, 인스타그램 릴스 등 숏폼 영상 크리에이터를 위한 **AI 기반 피드백 시스템**입니다.

사용자가 업로드한 댄스 챌린지 영상을 분석하여 **바이럴 가능성 예측**, **동작 피드백**, **제목/썸네일 생성** 등 종합적인 콘텐츠 최적화 서비스를 제공합니다.

### 🎯 What Makes TrendIT Special?

| Feature | Description |
|---------|-------------|
| 🧠 **Intelligent Intent Routing** | 사용자 의도를 자동 분류하여 최적의 워크플로우로 안내 |
| 📊 **ML-Powered Virality Prediction** | CatBoost + SHAP 기반 바이럴 가능성 예측 |
| 🕺 **Motion Analysis** | MediaPipe Pose로 레퍼런스 vs 사용자 동작 비교 분석 |
| 🎨 **AI Thumbnail Generation** | Generative AI 기반 맞춤형 썸네일 자동 생성 |
| 💬 **Conversational Interface** | LLM 기반 자연스러운 대화형 피드백 제공 |

---

## 🏗 Architecture

### 🔄 Workflow Steps Explained

| Step | Node | Description |
|------|------|-------------|
| **1** | `list_guide_videos` | DB에서 가이드 영상 목록 조회 |
| **2** | `select_reference` | Semantic Search로 레퍼런스 영상 선택 |
| **3** | `upload_video` | 사용자 영상 업로드 (Blob Storage) |
| **4** | `analyze_features` | CatBoost 예측 + SHAP + Gemini 상세 분석 |
| **5** | `feedback_type_router` | 사용자 선택 기반 피드백 유형 분기 |
| **6** | `motion_feedback` | MediaPipe 포즈 분석 + 동작 피드백 |
| **7** | `title_generator` | RAG + 트렌드 밈 기반 제목 생성 |
| **8** | `generate_thumbnail` | Generative AI 썸네일 생성 |

---

## 📂 Project Structure

```
TrendIT-backend/
├── 📁 app/
│   ├── 📁 agent/                    # 🤖 LangGraph Agent Core
│   │   ├── agent_state.py          # State Schema Definition
│   │   ├── graph.py                # Graph Construction & Routing
│   │   ├── nodes.py                # Node Functions (8-Step Logic)
│   │   └── prompts.py              # LLM Prompt Templates
│   │
│   ├── 📁 api/                      # 🌐 API Endpoints
│   │   └── v1/
│   │       └── endpoints/
│   │           ├── agent.py        # Agent Chat API
│   │           ├── chat.py         # Chat API
│   │           ├── predict.py      # ML Prediction API
│   │           └── analyze.py      # Video Analysis API
│   │
│   ├── 📁 services/                 # ⚙️ Business Logic Services
│   │   ├── agent/
│   │   │   └── service.py          # AgentApiService
│   │   ├── analyze/
│   │   │   └── service.py          # AnalyzeApiService
│   │   ├── motion_feedback.py      # MediaPipe Motion Analysis
│   │   ├── phi_service.py          # LLM Service (Phi/Gemini)
│   │   ├── gemini_service.py       # Gemini API Wrapper
│   │   └── vector_store.py         # ChromaDB Vector Store
│   │
│   ├── 📁 models/                   # 📊 ML Models & DB Models
│   └── 📁 core/                     # 🔧 Core Configuration
│
├── 📁 docs/                         # 📚 Documentation
│   └── 📁 images/                   # Architecture Diagrams
│
├── 📁 guide_videos/                 # 🎥 Reference Videos
├── 📁 rag_docs/                     # 📄 RAG Documents
├── 📁 chroma_db/                    # 💾 Vector Database
│
├── 📄 requirements.txt              # Dependencies
├── 📄 .env                          # Environment Variables
└── 📄 README.md                     # This file
```

---

## 🚀 Quick Start

### Prerequisites

- Python 3.11+
- PostgreSQL (or SQLite for development)
- CUDA-enabled GPU (recommended for MediaPipe)

### 1️⃣ Clone & Setup

```bash
# Clone the repository
git clone https://github.com/your-org/TrendIT-backend.git
cd TrendIT-backend

# Create virtual environment
python -m venv venv
.\venv\Scripts\activate  # Windows
# source venv/bin/activate  # Linux/Mac

# Install dependencies
pip install -r requirements.txt
```

### 2️⃣ Environment Configuration

```bash
# Copy and edit .env file
cp .env.example .env
```

```env
# .env
DATABASE_URL=postgresql://user:password@localhost:5432/trendit
GEMINI_API_KEY=your_gemini_api_key_here
GROQ_API_KEY=your_groq_api_key_here
VIDEO_STORAGE_DIR=./storage/videos
GUIDE_VIDEOS_DIR=./guide_videos
```

### 3️⃣ Run the Server

```bash
# Start FastAPI server
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

### 4️⃣ Access the API

- **API Documentation**: http://localhost:8000/docs
- **Agent Chat Endpoint**: `POST /api/v1/agent/chat`

---

## �️ Frontend Setup

This repository includes the frontend application in `trendit_front/`.

### Prerequisites

- Node.js 18+
- npm or yarn

### 1️⃣ Install Dependencies

```bash
cd trendit_front
npm install
```

### 2️⃣ Configure Environment

```bash
cp .env.example .env
```

Edit `.env` with your configuration:
```env
NEXT_PUBLIC_API_BASE=http://localhost:8000
BACKEND_BASE_URL=http://localhost:8000
NEXT_PUBLIC_GOOGLE_CLIENT_ID=your_google_client_id_here
```

### 3️⃣ Run Development Server

```bash
npm run dev
```

- **Frontend**: http://localhost:3000

---


## �💬 API Usage

### Chat with Agent

```bash
curl -X POST "http://localhost:8000/api/v1/agent/chat" \
  -H "Content-Type: application/json" \
  -d '{
    "message": "가이드 영상 목록 보여줘",
    "thread_id": "session-123"
  }'
```

### Response Example

```json
{
  "response": "📹 **사용 가능한 가이드 영상 목록입니다:**\n\n1. [상] **겨울에는 첫눈 챌린지 ❄️**...\n2. [중상] **lovelovelove 챌린지**...\n\n원하시는 영상의 제목이나 번호를 입력해주세요!",
  "intent": "guide",
  "workflow_stage": "awaiting_guide_selection"
}
```

---

## 🧪 Demo & Visualization

### Jupyter Notebook Demo

```bash
# Activate venv first
.\venv\Scripts\activate

# Install Jupyter
pip install jupyter

# Run visualization notebook
jupyter notebook agent_visualization.ipynb
```

### Python Script Demo

```python
from app.agent.graph import build_trendit_agent_graph_no_interrupt

# Build the agent graph
graph = build_trendit_agent_graph_no_interrupt()

# Run a query
result = graph.invoke({
    "user_query": "가이드 영상 보여줘",
    "conversation_history": []
})

print(result["final_response"])
```

---

## 🔧 Core Components

### 🤖 Agent State Schema

```python
class AgentState(TypedDict, total=False):
    # User Input
    user_query: str
    intent: Literal["chat", "guide", "feedback", "upload", "title", "thumbnail"]
    
    # Video Paths
    gt_video_path: Optional[str]      # Reference video
    user_video_path: Optional[str]    # User uploaded video
    
    # Analysis Results
    feature_analysis: Optional[dict]
    virality_label: Optional[Literal["viral", "stagnant"]]
    
    # Feedback Options
    feedback_type: Optional[Literal["motion", "title", "lighting"]]
    motion_feedback_json: Optional[str]
    
    # Output
    final_response: Optional[str]
```

### 🔀 Intent Router Logic

| Intent | Trigger Keywords | Next Node |
|--------|-----------------|-----------|
| `chat` | 일반 대화 | `chat` → `END` |
| `guide` | "가이드", "영상 목록" | `list_guide_videos` |
| `feedback` | "피드백", "분석해줘" | `feedback_type_router` |
| `title` | "제목", "타이틀" | `title_generator` |
| `thumbnail` | "썸네일", "미리보기" | `generate_thumbnail` |

---

## 📊 ML Pipeline

### Virality Prediction

```
User Video → Feature Extraction → CatBoost Model → SHAP Analysis
                  ↓
            [Motion, Lighting, Audio, Background, Composition]
                  ↓
            Virality Score (0-100%) + Top Strengths/Weaknesses
```

### Motion Feedback

```
Reference Video + User Video → MediaPipe Pose Extraction
                  ↓
            DTW Similarity Analysis
                  ↓
            Per-Frame Feedback + Overall Score
```

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 🙏 Acknowledgements

- [LangGraph](https://github.com/langchain-ai/langgraph) - Stateful Agent Framework
- [MediaPipe](https://mediapipe.dev/) - Pose Estimation
- [Google Gemini](https://ai.google.dev/) - Multimodal AI
- [FastAPI](https://fastapi.tiangolo.com/) - API Framework
- [CatBoost](https://catboost.ai/) - ML Model

---

<p align="center">
  Made with ❤️ by the TrendIT Team
</p>

<p align="center">
  <a href="#top">⬆️ Back to Top</a>
</p>
