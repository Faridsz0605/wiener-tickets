# Wiener Tickets - MLOps: Customer Service Ticket Prediction

This repository is a fork of the [MLOps course by Platzi](https://github.com/platzi/Mlops-platzi), adapted by **Wiener Studios** to build an end-to-end MLOps pipeline for intelligent prediction and routing of customer service tickets using NLP.

The course is guided by **Mera Camila Durango**, ML Engineer with experience at Mercado Libre and active contributor to the Medellin AI community. The goal is to shift the data-science mindset toward comprehensive model management: automating training pipelines, tracking experiments, serving predictions in real time, and detecting model degradation before it impacts the end user.

## How It Works

The following diagram illustrates the full pipeline, from raw customer feedback to production inference and monitoring:

<p align="center">
  <img src="public/exali-diagram-wf" alt="MLOps Pipeline Architecture" width="860"/>
</p>

The pipeline covers three phases:

1. **Development and Experimentation** - Data extraction from CRM, preprocessing (tokenization, cleaning), model training with iterative experimentation, and model registry.
2. **Continuous Integration and Delivery** - Automated tests on code push, Docker image builds, and staging deployment.
3. **Operations and Production** - Containerized model served via FastAPI, real-time inference, monitoring for data drift and model decay, and a feedback loop that triggers retraining.

## Tools and Setup

For dependency and package management we use [uv](https://docs.astral.sh/uv/), a fast Python package manager that handles dependencies, virtual environments, and lockfiles.

For managing Python and tool versions we use [mise-en-place](https://mise.jdx.dev/), which lets us pin runtime versions per project via a `.mise.toml` file.

### Prerequisites

- [mise](https://mise.jdx.dev/getting-started.html)
- [uv](https://docs.astral.sh/uv/getting-started/installation/)
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

# Run a script
uv run python src/train.py
```

## Repository Structure

The repository has two main branches:

- `main` — covers tracking and orchestration topics.
- `deploy_prod` — everything related to deploying a machine learning model to production.

Key directories:

```
wiener-tickets/
├── src/               # Source code for data processing and model training
├── notebooks/         # Exploratory analysis and prototyping
├── tracking/          # Experiment tracking configuration (MLflow)
├── orchestration/     # Pipeline orchestration
├── public/            # Static assets (diagrams, images)
├── utils/             # Shared utilities and helpers
├── .mise.toml         # mise version management
├── pyproject.toml     # uv dependency management
├── uv.lock            # uv lockfile
└── README.md
```

## Experiment Tracking

We use **MLflow** for experiment tracking — logging metrics, hyperparameters, and model versions systematically.

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

## Instructor

**Mera Camila Durango** — ML Engineer with experience at Mercado Libre and active contributor to the Medellin AI community. Specialises in taking ML models from prototype to production-grade MLOps systems.

## License

MIT License — see [LICENSE](LICENSE) for details.
