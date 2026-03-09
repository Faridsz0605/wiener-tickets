<h1 align="center">Wiener Tickets — MLOps for Customer Service</h1>

<p align="center">
  Intelligent prediction and routing of customer service tickets using NLP and end-to-end MLOps
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-active-brightgreen?style=for-the-badge" alt="Status">
  <img src="https://img.shields.io/badge/python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/MLflow-experiment%20tracking-0194E2?style=for-the-badge&logo=mlflow&logoColor=white" alt="MLflow">
  <img src="https://img.shields.io/badge/FastAPI-serving-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI">
  <img src="https://img.shields.io/badge/Docker-containerized-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white" alt="CI/CD">
  <img src="https://img.shields.io/badge/license-MIT-yellow?style=for-the-badge" alt="License">
</p>

---

## About

**Wiener Tickets** is a production-grade implementation of the complete **MLOps lifecycle**, focused on the intelligent prediction and automatic routing of customer service tickets using Natural Language Processing applied to raw customer feedback — complaints, comments, and support requests.

The project is guided by **Mera Camila Durango**, ML Engineer with experience at Mercado Libre and active contributor to the Medellin AI community. The goal is to shift the data-science mindset toward comprehensive model management: automating training pipelines, tracking experiments, serving predictions in real time, and detecting model degradation before it impacts the end user.

---

## Architecture

<p align="center">
  <img src="docs/assets/mlops_pipeline.png" alt="MLOps Pipeline Architecture" width="860"/>
</p>

The pipeline runs across three distinct phases:

```
PHASE 1 — Development & Experimentation

  CRM Database → Preprocessing Pipeline → Model Training → Model Registry
                  (tokenization, cleaning)   (iterative loop)


PHASE 2 — Continuous Integration & Delivery

  GitHub Repo → Automated Tests → Build & Package → Staging Deploy
  (code push)   (unit + data val)  (Docker image)    (pre-prod env)


PHASE 3 — Operations & Production

  Containerised Model → FastAPI Endpoint → Client Application (CRM)
  (Docker + registry)   (real-time inference)        |
                                                      | feedback loop
  Monitoring & Alerting ← Data Collection (new labelled tickets)
  (drift / decay alerts)        |
                                └──────────────────→ Phase 1 (retrain)
```

---

## Key Components

| Component | Description |
|-----------|-------------|
| DataOps | Extraction, cleaning, and tokenization of unstructured text (complaints and comments) |
| Experiment Tracking | Systematic logging of metrics, hyperparameters, and model versions with MLflow or Weights & Biases |
| CI/CD for ML | Automated training and deployment pipelines triggered on code or data changes |
| Model Serving | Containerised model (Docker) exposed via a FastAPI REST API for real-time inference |
| Continuous Monitoring | Data-drift and model-decay detection with automated retraining triggers |

---

## Getting Started

### Prerequisites

- Python >= 3.10
- Docker and Docker Compose
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/Faridsz0605/wiener-tickets.git
cd wiener-tickets

# Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Training

```bash
# Train the NLP model and log the run to MLflow
python src/train.py

# Launch the MLflow tracking UI
mlflow ui
```

### Serving

```bash
# Build and start the API with Docker Compose
docker compose up --build

# REST API available at:
# http://localhost:8000/docs
```

---

## Project Structure

```
wiener-tickets/
├── data/
│   ├── raw/                 # Raw customer feedback dumps
│   └── processed/           # Cleaned and tokenised datasets
├── docs/
│   └── assets/              # Images, diagrams, and design docs
├── models/                  # Serialised model artefacts
├── notebooks/               # Exploratory analysis and prototyping
├── src/
│   ├── data/                # DataOps: ingestion and preprocessing
│   ├── features/            # Feature engineering and NLP utilities
│   ├── models/              # Training scripts and model definitions
│   ├── api/                 # FastAPI application and endpoints
│   └── monitoring/          # Drift detection and alerting
├── tests/                   # Unit and integration tests
├── .github/workflows/       # CI/CD pipeline definitions
├── docker-compose.yml
├── Dockerfile
└── requirements.txt
```

---

## Testing

```bash
pytest tests/ -v --cov=src
```

---

## Experiment Tracking

```bash
# MLflow (local)
export MLFLOW_TRACKING_URI=http://localhost:5000
mlflow server --backend-store-uri sqlite:///mlflow.db --default-artifact-root ./mlruns

# Weights & Biases
wandb login
python src/train.py --tracker wandb
```

---

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feat/your-feature`
3. Commit your changes using conventional commits: `git commit -m "feat: add your feature"`
4. Push the branch: `git push origin feat/your-feature`
5. Open a Pull Request

---

## Instructor

**Mera Camila Durango** — ML Engineer with experience at Mercado Libre and active contributor to the Medellin AI community. Specialises in taking ML models from prototype to production-grade MLOps systems.

---

## License

MIT License — see [LICENSE](LICENSE) for details.
