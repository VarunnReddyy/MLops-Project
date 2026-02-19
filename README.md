# 🚗 End-to-End MLOps Vehicle Data Pipeline

![Python](https://img.shields.io/badge/Python-3.10-3776AB?style=for-the-badge&logo=python&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-EC2%20%7C%20S3%20%7C%20ECR-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI%2FCD-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)

## 📌 Project Overview
This project demonstrates a production-ready, end-to-end Machine Learning Operations (MLOps) pipeline for vehicle data prediction. It bridges the gap between Jupyter Notebook experimentation and cloud-based production systems. 

The architecture seamlessly handles everything from automated data ingestion (via MongoDB) to model training, evaluation, and CI/CD deployment on an AWS EC2 instance using Docker and GitHub Actions.



---

## 🛠️ Tech Stack & Tools
* **Language:** Python 3.10
* **Database:** MongoDB Atlas (Cloud)
* **Cloud Provider:** Amazon Web Services (AWS - S3, IAM, ECR, EC2)
* **Containerization:** Docker
* **CI/CD:** GitHub Actions (Self-hosted runner)
* **Web App:** Flask/FastAPI 

---

## 🏗️ Pipeline Architecture (How it Works)

This project is built using a highly modular component-based architecture to ensure scalability and reproducibility. 

### 1. Data Ingestion & Database Setup
* Connected to a remote **MongoDB Atlas** cluster using `pymongo`.
* Automated data extraction from NoSQL collections into Pandas DataFrames.
* Train/Test split logic is executed and raw datasets are saved into a local `artifact/` feature store.

### 2. Data Validation & Transformation
* **Validation:** Automated checks against a predefined `schema.yaml` to ensure incoming data structure matches model expectations.
* **Transformation:** Feature engineering, encoding, and scaling pipelines are applied. The `preprocessor.pkl` object is saved for future API inferences.

### 3. Model Training & Evaluation
* The system trains the model and evaluates it against current production thresholds (e.g., `MODEL_EVALUATION_CHANGED_THRESHOLD_SCORE: 0.02`).
* If the newly trained model outperforms the current production model, it is accepted for deployment.

### 4. Model Pusher (AWS S3 Model Registry)
* Integrates securely with **AWS S3** (`my-model-mlopsproj` bucket).
* Approved models and preprocessors are pushed directly to the S3 bucket, serving as an automated Model Registry.

---

## 🚀 CI/CD & Deployment Flow

The deployment process is entirely automated via **GitHub Actions** and **Docker**.

1. **Continuous Integration (CI):** Upon push to the `main` branch, GitHub Actions triggers a workflow to lint code and build a Docker Image.
2. **Container Registry:** The successful build is pushed to an **AWS ECR** (Elastic Container Registry) repository.
3. **Continuous Deployment (CD):** A self-hosted GitHub runner stationed on an **AWS EC2 Ubuntu Server** pulls the latest Docker image from ECR and runs it on port `5080`.
4. **Serving:** The web application becomes accessible globally via the EC2 Public IP.

---

## 💻 How to Run Locally

If you wish to clone and test this pipeline on your local machine, follow these steps:

### 1. Prerequisites
Ensure you have Python 3.10 installed. Create and activate a conda virtual environment:
```bash
conda create -n vehicle python=3.10 -y
conda activate vehicle

```

### 2. Install Dependencies

Install the required local packages and libraries:

```bash
pip install -r requirements.txt
python setup.py install 

```

### 3. Setup Environment Variables

You will need your own MongoDB cluster and AWS IAM credentials with Administrator Access. Export them in your terminal:

**For Mac/Linux:**

```bash
export MONGODB_URL="mongodb+srv://<username>:<password>@cluster..."
export AWS_ACCESS_KEY_ID="your_access_key"
export AWS_SECRET_ACCESS_KEY="your_secret_key"
export AWS_DEFAULT_REGION="us-east-1"

```

### 4. Execute the Pipeline

To run the automated pipeline (Ingestion -> Training -> Evaluation):

```bash
python demo.py

```

To launch the web application interface locally:

```bash
python app.py



