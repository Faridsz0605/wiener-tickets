# Wiener Tickets - MLOps: Customer Service Ticket Prediction

This repository is a fork of the [MLOps course by Platzi](https://github.com/platzi/Mlops-platzi), adapted by **Wiener Studios** to build an end-to-end MLOps pipeline for intelligent prediction and routing of customer service tickets using NLP.

The course is guided by **Mera Camila Durango**, ML Engineer with experience at Mercado Libre and active contributor to the Medellin AI community. The goal is to shift the data-science mindset toward comprehensive model management: automating training pipelines, tracking experiments, serving predictions in real time, and detecting model degradation before it impacts the end user.
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

## How It Works

The following diagram illustrates the full pipeline, from raw customer feedback to production inference and monitoring:

[![MLOps Pipeline Architecture](https://img.shields.io/badge/View%20Diagram-Excalidraw-6965db?style=for-the-badge&logo=excalidraw&logoColor=white)](https://excalidraw.com/#json=u8Z8X1b1AwEMDf_YUf7W2,NB5lk3d9MyfpAh2NVsH0Mw)

The pipeline covers three phases:
## About

**Wiener Tickets** is a production-grade implementation of the complete **MLOps lifecycle**, focused on the intelligent prediction and automatic routing of customer service tickets using Natural Language Processing applied to raw customer feedback — complaints, comments, and support requests.

The project is guided by **Mera Camila Durango**, ML Engineer with experience at Mercado Libre and active contributor to the Medellin AI community. The goal is to shift the data-science mindset toward comprehensive model management: automating training pipelines, tracking experiments, serving predictions in real time, and detecting model degradation before it impacts the end user.

1. **Development and Experimentation** - Data extraction from CRM, preprocessing (tokenization, cleaning), model training with iterative experimentation, and model registry.
2. **Continuous Integration and Delivery** - Automated tests on code push, Docker image builds, and staging deployment.
3. **Operations and Production** - Containerized model served via FastAPI, real-time inference, monitoring for data drift and model decay, and a feedback loop that triggers retraining.

## Tools and Setup

For dependency and package management we use [uv](https://docs.astral.sh/uv/), a fast Python package manager that handles dependencies, virtual environments, and lockfiles.

For managing Python and tool versions we use [mise-en-place](https://mise.jdx.dev/), which lets us pin runtime versions per project via a `.mise.toml` file.

### Prerequisites

- [mise](https://mise.jdx.dev/getting-started.html)
- [uv](https://docs.astral.sh/uv/getting-started/installation/)
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

### Getting Started

```bash
# Clone the repository
git clone https://github.com/Faridsz0605/wiener-tickets.git
cd wiener-tickets

# Install the correct Python version via mise
mise install

# Install dependencies with uv
uv sync
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

# Run a script
uv run python src/train.py
```

## Repository Structure

The repository has two main branches:
### Serving

```bash
# Build and start the API with Docker Compose
docker compose up --build

# REST API available at:
# http://localhost:8000/docs
```

- `master` / `main` — covers tracking and orchestration topics.
- `deploy_prod` — everything related to deploying a machine learning model to production.

Key directories:

```
wiener-tickets/
├── src/               # Source code for data processing and model training
├── notebooks/         # Exploratory analysis and prototyping
├── tracking/          # Experiment tracking configuration (MLflow)
├── orchestration/     # Pipeline orchestration (Prefect / Airflow)
├── utils/             # Shared utilities and helpers
├── .mise.toml         # mise version management
├── pyproject.toml     # uv dependency management
├── uv.lock            # uv lockfile
└── README.md
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

## Experiment Tracking

We use **MLflow** for experiment tracking — logging metrics, hyperparameters, and model versions systematically.
## Experiment Tracking

```bash
# Start the MLflow tracking server
mlflow server --backend-store-uri sqlite:///mlflow.db --default-artifact-root ./mlruns

# Access the UI at http://localhost:5000
```

## Important Notes

- Generated data is sensitive. Store datasets securely (S3 bucket or equivalent). Repositories should only contain code, not data.
- Put your ML knowledge to work: hyperparameter validation, underfitting/overfitting detection, feature engineering, dimensionality reduction.
- For compute-heavy workloads, consider cloud resources, Dask for parallelism, Spark clusters, or multiprocessing. Process data in chunks when needed.

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feat/your-feature`
3. Commit using conventional commits: `git commit -m "feat: add your feature"`
4. Push and open a Pull Request
3. Commit your changes using conventional commits: `git commit -m "feat: add your feature"`
4. Push the branch: `git push origin feat/your-feature`
5. Open a Pull Request

---

## Instructor

**Mera Camila Durango** — ML Engineer with experience at Mercado Libre and active contributor to the Medellin AI community. Specialises in taking ML models from prototype to production-grade MLOps systems.

---

## License

MIT License — see [LICENSE](LICENSE) for details.
