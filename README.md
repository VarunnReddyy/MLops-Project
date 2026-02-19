# 🚗 End-to-End MLOps Vehicle Data Pipeline

![Python](https://img.shields.io/badge/Python-3.10-3776AB?style=for-the-badge&logo=python&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-EC2%20%7C%20S3%20%7C%20ECR-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI%2FCD-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)

## 📌 Project Overview
Welcome to this MLOps project, designed to demonstrate a robust pipeline for managing vehicle insurance data. This project aims to impress recruiters and visitors by showcasing the various tools, techniques, services, and features that go into building and deploying a machine learning pipeline for real-world data management. Follow along to learn about project setup, data processing, model deployment, and CI/CD automation!



---

## 🛠️ Tech Stack & Tools
* **Language:** Python 3.10
* **Database:** MongoDB Atlas (Cloud)
* **Cloud Provider:** Amazon Web Services (AWS - S3, IAM, ECR, EC2)
* **Containerization:** Docker
* **CI/CD:** GitHub Actions (Self-hosted runner)
* **Web App:** Flask/FastAPI 

---

## 📁 Project Setup and Structure

**Step 1: Project Template**
Start by executing the `template.py` file to create the initial project template, which includes the required folder structure and placeholder files.

**Step 2: Package Management**
Write the setup for importing local packages in the `setup.py` and `pyproject.toml` files.
*Tip: Learn more about these files from `crashcourse.txt`.*

**Step 3: Virtual Environment and Dependencies**
Create a virtual environment and install required dependencies from `requirements.txt`:
```bash
conda create -n vehicle python=3.10 -y
conda activate vehicle
pip install -r requirements.txt

```

Verify the local packages by running:

```bash
pip list

```

---

## 📊 MongoDB Setup and Data Management

**Step 4: MongoDB Atlas Configuration**

* Sign up for **MongoDB Atlas** and create a new project.
* Set up a free `M0` cluster, configure the username and password, and allow access from any IP address (`0.0.0.0/0`).
* Retrieve the MongoDB connection string for Python and save it (replace `<password>` with your password).

**Step 5: Pushing Data to MongoDB**

* Create a folder named `notebook`, add the dataset, and create a notebook file `mongoDB_demo.ipynb`.
* Use the notebook to push data to the MongoDB database.
* Verify the data in MongoDB Atlas under **Database > Browse Collections**.

---

## 📝 Logging, Exception Handling, and EDA

**Step 6: Set Up Logging and Exception Handling**
Create logging and exception handling modules. Test them on a demo file `demo.py`.

**Step 7: Exploratory Data Analysis (EDA) and Feature Engineering**
Analyze and engineer features in the **EDA** and **Feature Engg** notebook for further processing in the pipeline.

---

## 📥 Data Ingestion

**Step 8: Data Ingestion Pipeline**

* Define MongoDB connection functions in `configuration.mongo_db_connections.py`.
* Develop data ingestion components in the `data_access` and `components.data_ingestion.py` files to fetch and transform data.
* Update `entity/config_entity.py` and `entity/artifact_entity.py` with relevant ingestion configurations.
* Run `demo.py` after setting up the MongoDB connection as an environment variable.

**Setting Environment Variables**
Set your MongoDB URL:

```bash
# For Bash (Mac/Linux)
export MONGODB_URL="mongodb+srv://<username>:<password>...."

# For PowerShell (Windows)
$env:MONGODB_URL="mongodb+srv://<username>:<password>...."

```

*Note: On Windows, you can also set environment variables through the system settings. Also, add the `artifact` dir to your `.gitignore` file.*

---

## 🔍 Data Validation, Transformation & Model Training

**Step 9: Data Validation**
Define the schema in `config.schema.yaml` and implement data validation functions in `utils.main_utils.py`.

**Step 10: Data Transformation**
Implement data transformation logic in `components.data_transformation.py` and create `estimator.py` in the `entity` folder.

**Step 11: Model Training**
Define and implement model training steps in `components.model_trainer.py` using code from `estimator.py`.

---

## 🌐 AWS Setup for Model Evaluation & Deployment

**Step 12: AWS Setup**

* Log in to the AWS console, create an IAM user, and grant **AdministratorAccess**.
* Set AWS credentials as environment variables:

```bash
# For Bash
export AWS_ACCESS_KEY_ID="YOUR_AWS_ACCESS_KEY_ID"
export AWS_SECRET_ACCESS_KEY="YOUR_AWS_SECRET_ACCESS_KEY"

```

* Configure the S3 Bucket and add access keys in `constants.__init__.py`. Ensure the following thresholds and bucket names are set:
* `MODEL_EVALUATION_CHANGED_THRESHOLD_SCORE: 0.02`
* `MODEL_BUCKET_NAME = "my-model-mlopsproj"`
* `MODEL_PUSHER_S3_KEY = "model-registry"`



**Step 13: Model Evaluation and Pushing to S3**

* Create an S3 bucket named `my-model-mlopsproj` in the `us-east-1` region. Uncheck "Block all public access".
* Develop code to push/pull models to/from the S3 bucket in `src.aws_storage` and `entity/s3_estimator.py`.

---

## 🚀 Model Evaluation, Model Pusher, and Prediction Pipeline

**Step 14: Model Evaluation & Model Pusher**

* Implement model evaluation and deployment components.
* Create the **Prediction Pipeline** and set up `app.py` for API integration.

**Step 15: Static and Template Directory**
Add `static` and `template` directories for the web UI.

---

## 🔄 CI/CD Setup with Docker, GitHub Actions, and AWS

**Step 16: Docker and GitHub Actions**

* Create `Dockerfile` and `.dockerignore`.
* Set up GitHub Actions with AWS authentication by creating secrets in GitHub for:
* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`
* `AWS_DEFAULT_REGION`
* `ECR_REPO`



**Step 17: AWS EC2 and ECR**

* Create an ECR repository named `vehicleproj`.
* Set up an EC2 instance (Ubuntu Server, T2 Medium) for deployment.
* Install Docker on the EC2 machine.
* Connect EC2 as a self-hosted runner on GitHub.

**Step 18: Final Steps**

* Open the `5080` port on the EC2 instance's security group.
* Access the deployed app by visiting `http://<public_ip>:5080`.
* You can also do model training directly on the `/training` route.

---

## 🛠️ Additional Resources

* **Crash Course on setup.py and pyproject.toml:** See `crashcourse.txt` for details.
* **GitHub Secrets:** Manage secrets for secure CI/CD pipelines.

---

## 🎯 Project Workflow Summary

**Data Ingestion** ➔ **Data Validation** ➔ **Data Transformation** **Model Training** ➔ **Model Evaluation** ➔ **Model Deployment** **CI/CD Automation** with GitHub Actions, Docker, AWS EC2, and ECR

---

## 💬 Connect

If you found this project helpful or have any questions, feel free to reach out! This README provides a structured walkthrough of the MLOps project, showcasing the end-to-end pipeline, cloud integration, CI/CD setup, and robust data handling capabilities.

