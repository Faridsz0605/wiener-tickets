<h1 align="center">🎫 Wiener Tickets — MLOps for Customer Service</h1>

<p align="center">
  <em>Intelligent prediction and routing of customer service tickets using NLP & end-to-end MLOps</em>
</p>

<p align="center">
  <!-- Status -->
  <img src="https://img.shields.io/badge/status-active-brightgreen?style=for-the-badge" alt="Status">
  <!-- Python -->
  <img src="https://img.shields.io/badge/python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <!-- MLflow -->
  <img src="https://img.shields.io/badge/MLflow-experiment%20tracking-0194E2?style=for-the-badge&logo=mlflow&logoColor=white" alt="MLflow">
  <!-- FastAPI -->
  <img src="https://img.shields.io/badge/FastAPI-serving-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI">
  <!-- Docker -->
  <img src="https://img.shields.io/badge/Docker-containerized-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker">
  <!-- CI/CD -->
  <img src="https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white" alt="CI/CD">
  <!-- License -->
  <img src="https://img.shields.io/badge/license-MIT-yellow?style=for-the-badge" alt="License">
</p>

---

## 📸 Architecture Overview

> *Place your MLOps pipeline diagram here — see [Workflow Diagram](#-workflow-diagram) section for guidance on what to include.*

<p align="center">
  <img src="docs/assets/mlops_pipeline.png" alt="MLOps Pipeline Architecture" width="860"/>
</p>

---

## 📖 About the Project

**Wiener Tickets** provides a practical, production-grade implementation of the complete **Machine Learning Operations (MLOps)** lifecycle. The domain focus is on the **intelligent prediction and automatic routing of customer service tickets** by applying Natural Language Processing (NLP) to raw customer feedback — complaints, comments, and support requests.

Guided by **Mera Camila Durango** — a professional with experience at *Mercado Libre* and the *Medellín AI community* — this project teaches practitioners how to transition ML models from isolated local experiments into **scalable, monitored, and fully automated production environments**.

The primary goal is to shift the traditional data-science mindset toward **comprehensive model management**: automating training pipelines, tracking experiments, serving predictions in real time, and detecting model degradation before it hurts the end user.

---

## ✨ Key Components

| Component | Description |
|-----------|-------------|
| **DataOps** | Extraction, cleaning, and tokenization of unstructured text (complaints & comments) to prepare data for NLP algorithms |
| **Experiment Tracking** | Systematic logging of metrics, hyperparameters, and model versions with **MLflow** or **Weights & Biases** |
| **CI/CD for ML** | Automated training and deployment pipelines that re-evaluate and redeploy models whenever code or data changes |
| **Model Serving** | Containerised model (Docker) exposed through a **FastAPI** REST API for real-time inference by customer-service systems |
| **Continuous Monitoring** | Data-drift and model-decay detection with automated retraining triggers to maintain prediction quality over time |

---

## 🗺 Workflow Diagram

The MLOps pipeline is structured in **three distinct architectural phases**:

```
┌──────────────────────────────────────────────────────────────────────────────────┐
│  PHASE 1 · Development & Experimentation (Dev)                                   │
│                                                                                  │
│   CRM Database ──► Preprocessing Pipeline ──► Model Training ──► Model Registry │
│                         (tokenization,                (iterative                 │
│                          cleaning)                     loop)                     │
└──────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────────────┐
│  PHASE 2 · Continuous Integration & Delivery (CI/CD)                             │
│                                                                                  │
│   GitHub Repo ──► Automated Tests ──► Build & Package ──► Staging Deploy        │
│   (code push)      (unit + data         (Docker image)     (pre-prod env)        │
│                     validation)                                                  │
└──────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌──────────────────────────────────────────────────────────────────────────────────┐
│  PHASE 3 · Operations & Production (Ops)                                         │
│                                                                                  │
│   Containerised Model ──► FastAPI Endpoint ──► Client Application                │
│   (Docker + registry)      (real-time              (CRM / support tool)          │
│                             inference)                    │                      │
│                                                           │ feedback loop        │
│   Monitoring & Alerting ◄──────────────────── Data Collection                   │
│   (drift / decay alerts)                      (new labelled tickets)             │
│          │                                                                       │
│          └──────────────────────────────────────────► Phase 1 (retrain)         │
└──────────────────────────────────────────────────────────────────────────────────┘
```

> **Tip:** Use tools like [Excalidraw](https://excalidraw.com), [draw.io](https://draw.io), or [Mermaid](https://mermaid.js.org) to render this as a visual diagram and drop it into `docs/assets/mlops_pipeline.png`.

---

## 🚀 Getting Started

### Prerequisites

- Python ≥ 3.10
- Docker & Docker Compose
- Git

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/Faridsz0605/wiener-tickets.git
cd wiener-tickets

# 2. Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt
```

### Running the Experiment

```bash
# Train the NLP model and log the run to MLflow
python src/train.py

# Launch the MLflow tracking UI
mlflow ui
```

### Serving the Model

```bash
# Build and start the API with Docker Compose
docker compose up --build

# The REST API will be available at:
# http://localhost:8000/docs
```

---

## 📂 Project Structure

```
wiener-tickets/
├── data/
│   ├── raw/                 # Raw customer feedback dumps
│   └── processed/           # Cleaned & tokenised datasets
├── docs/
│   └── assets/              # Images, diagrams, and design docs
├── models/                  # Serialised model artefacts
├── notebooks/               # Exploratory analysis & prototyping
├── src/
│   ├── data/                # DataOps: ingestion & preprocessing
│   ├── features/            # Feature engineering & NLP utilities
│   ├── models/              # Training scripts & model definitions
│   ├── api/                 # FastAPI application & endpoints
│   └── monitoring/          # Drift detection & alerting
├── tests/                   # Unit and integration tests
├── .github/workflows/       # CI/CD pipeline definitions
├── docker-compose.yml
├── Dockerfile
└── requirements.txt
```

---

## 🧪 Running Tests

```bash
pytest tests/ -v --cov=src
```

---

## 📊 Experiment Tracking

This project supports both **MLflow** and **Weights & Biases** for tracking experiments.

```bash
# MLflow (local)
export MLFLOW_TRACKING_URI=http://localhost:5000
mlflow server --backend-store-uri sqlite:///mlflow.db --default-artifact-root ./mlruns

# Weights & Biases
wandb login
python src/train.py --tracker wandb
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "feat: add your feature"`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for coding standards and the development workflow.

---

## 👩‍🏫 Instructor

| | |
|---|---|
| **Mera Camila Durango** | ML Engineer with experience at **Mercado Libre** and active contributor to the **Medellín AI community**. Specialises in taking ML models from prototype to production-grade MLOps systems. |

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  Made with ❤️ for the Medellín AI community
  <br/>
  <img src="https://img.shields.io/badge/NLP-Customer%20Tickets-blueviolet?style=flat-square" alt="NLP">
  <img src="https://img.shields.io/badge/MLOps-End--to--End-orange?style=flat-square" alt="MLOps">
  <img src="https://img.shields.io/badge/Made%20in-Medell%C3%ADn%20🇨🇴-yellow?style=flat-square" alt="Medellín">
</p>
