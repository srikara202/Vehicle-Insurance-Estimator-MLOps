# MLOps Project: End-to-End Vehicle Insurance Prediction Pipeline

Welcome to the **Vehicle Insurance Prediction MLOps Project** — a robust, production-grade implementation of a machine learning pipeline following industry-standard MLOps practices. This project is built with a focus on automation, scalability, maintainability, and deployment to cloud infrastructure with CI/CD integration. Perfect to showcase your skills to recruiters and hiring managers.

---

## 🌟 Features at a Glance

* **Local Packaging** with `setup.py` and `pyproject.toml`
* **MongoDB Atlas** for NoSQL cloud database storage
* **Custom Logging** and **Exception Handling** modules
* **EDA & Feature Engineering** in Jupyter Notebooks
* **Data Ingestion, Validation, Transformation, Training** with modularized components
* **AWS Integration** for S3 model storage and IAM user access
* **Docker + GitHub Actions** for CI/CD
* **Live Prediction API** hosted on EC2 with a custom `/training` route

---

## ⚡ Project Setup Instructions

### 1. Project Bootstrap

* Run `template.py` to scaffold your project structure
* Use `setup.py` and `pyproject.toml` to package and manage your custom modules

### 2. Environment Setup

```bash
conda create -n vehicle python=3.10 -y
conda activate vehicle
pip install -r requirements.txt
pip list  # Verify package installation
```

---

## 📂 MongoDB Atlas Setup

1. Create a MongoDB Atlas project and M0 cluster
2. Set DB username/password and allow IP `0.0.0.0/0`
3. Get connection string from **Drivers** tab (choose Python)
4. Store and secure this URI in your environment variables:

```bash
# Bash
export MONGODB_URL="<your-mongodb-uri>"

# PowerShell
$env:MONGODB_URL = "<your-mongodb-uri>"
```

5. Push dataset to MongoDB via `mongoDB_demo.ipynb` in the `notebook/` folder

---

## 📈 Logging, Exception Handling & EDA

* Custom `logger.py` and `exception.py` files tested via `demo.py`
* EDA and Feature Engineering notebooks ready for analysis

---

## 📊 Data Ingestion Pipeline

1. Setup constants in `constants/__init__.py`
2. Configure DB connection in `configuration/mongo_db_connection.py`
3. Pull and convert MongoDB data to DataFrame using `data_access/proj1_data.py`
4. Define config and artifact schemas:

   * `entity/config_entity.py`
   * `entity/artifact_entity.py`
5. Run and verify via `demo.py`

---

## 🏛️ Data Validation, Transformation, and Training

1. Define schema in `config/schema.yaml`
2. Implement validation logic in `components/data_validation.py`
3. Build `estimator.py` inside `entity/` for transformation + training
4. Complete `model_trainer.py` for model fitting

---

## ☁️ AWS S3 & IAM Integration

1. IAM User Setup:

   * Region: `us-east-1`
   * Policy: `AdministratorAccess`
   * Create access keys & export to env:

```bash
# Bash
export AWS_ACCESS_KEY_ID=...
export AWS_SECRET_ACCESS_KEY=...

# PowerShell
$env:AWS_ACCESS_KEY_ID=...
$env:AWS_SECRET_ACCESS_KEY=...
```

2. S3 Bucket Setup:

   * Name: `my-model-mlopsproj`
   * Uncheck "Block all public access"
3. Store metadata in `constants/__init__.py`
4. Connect using `configuration/aws_connection.py` and `aws_storage/`
5. Manage models via `entity/s3_estimator.py`

---

## 🎯 Model Evaluation & Pushing

* Compare new model with existing S3 model
* Push best model to `model-registry` key in the S3 bucket

---

## 🚀 Prediction Pipeline

* Define routes in `app.py` for UI and `/training` for model retraining
* Serve predictions through Flask app hosted on EC2

```bash
/project
  |- static/
  |- templates/
  |- app.py
```

---

## 🚧 CI/CD Deployment with Docker + GitHub Actions

### Docker Setup

* `Dockerfile` and `.dockerignore` created
* Build and push to AWS ECR

### GitHub Actions

1. Add IAM User (e.g. `usvisa-user`) with access keys
2. Create GitHub secrets:

   * `AWS_ACCESS_KEY_ID`
   * `AWS_SECRET_ACCESS_KEY`
   * `AWS_DEFAULT_REGION`
   * `ECR_REPO`
3. Workflow file: `.github/workflows/aws.yaml`

---

## 📱 EC2 Hosting Instructions

1. Launch Ubuntu EC2 Instance (T2 Medium)
2. Install Docker:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
```

3. Setup GitHub Self-Hosted Runner
4. Open EC2 Inbound Rules (Port: 5080)
5. Access app at `http://<EC2-Public-IP>:5080`

---

## 🔄 Project Workflow Summary

```txt
constants/        # Environment & config constants
config_entity/    # Configuration schema
artifact_entity/  # Artifact schema
components/       # Core ML pipeline components
pipeline/         # Training and prediction pipelines
app.py / demo.py  # Serving and testing entrypoints
```

---

## 🎉 That's a Wrap!

This project serves as a **complete MLOps showcase**, highlighting real-world practices from development to deployment. Impress recruiters by demonstrating:

* ML pipeline design
* Database integration
* Scalable cloud deployment
* CI/CD workflows

> Feel free to fork, star, and extend the project!

---

## ✨ Made with Passion for MLOps
