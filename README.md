# Sentiment Analysis MLOps Project

This project implements a sentiment analysis application, demonstrating a full MLOps lifecycle. The application analyzes text input (e.g., movie reviews) and predicts the sentiment (positive/negative). It is designed to be deployed on AWS EKS (Elastic Kubernetes Service).

## Project Overview

The core functionality involves:
1.  **Data Ingestion & Preprocessing**: Fetching and cleaning text data.
2.  **Feature Engineering**: Transforming text data into numerical features suitable for machine learning models (e.g., TF-IDF).
3.  **Model Training & Evaluation**: Training a sentiment analysis model (e.g., Logistic Regression, or others) and evaluating its performance.
4.  **Model Versioning**: Using DVC to version data, models, and intermediate artifacts.
5.  **Experiment Tracking**: Using MLflow to log experiments, parameters, and metrics.
6.  **API Development**: A Flask application to serve the trained model via a REST API.
7.  **Containerization**: Dockerizing the Flask application for consistent deployment.
8.  **Orchestration & Deployment**: Deploying the containerized application to a Kubernetes cluster (AWS EKS) managed via Ansible.

## Technologies Used

This project leverages a variety of tools and technologies:

### Core Machine Learning & Data Processing
*   **Python 3.10**: Primary programming language.
*   **Scikit-learn**: For machine learning algorithms (e.g., Logistic Regression, TF-IDF Vectorizer) and model evaluation.
*   **Pandas**: For data manipulation and analysis.
*   **NumPy**: For numerical operations.
*   **NLTK**: For natural language processing tasks like stopword removal and lemmatization.

### MLOps & Workflow
*   **DVC (Data Version Control)**: For versioning datasets, models, and ML pipeline artifacts. Ensures reproducibility.
*   **MLflow**: For tracking experiments, packaging code into reproducible runs, and managing models.
*   **Makefile**: For automating common development tasks (e.g., setting up environments, running linters).

### Application & API
*   **Flask**: Micro web framework for creating the REST API to serve the sentiment analysis model.
*   **Gunicorn**: WSGI HTTP server for running the Flask application in production.

### Containerization & Orchestration
*   **Docker**: For containerizing the Flask application and its dependencies.
*   **Kubernetes**: For orchestrating containerized applications. The `deployment.yaml` file defines the deployment and service for Kubernetes.
*   **AWS EKS (Elastic Kubernetes Service)**: Managed Kubernetes service on AWS where the application is deployed.
*   **AWS ECR (Elastic Container Registry)**: Used to store the Docker image for the application.

### CI/CD & Automation
*   **Ansible**: For automating the deployment process to AWS EKS. The `ansible/` directory contains playbooks and roles for this purpose.
*   **Git**: For version control of the codebase.
*   **GitHub Actions** CI/CD pipeline


## Deployment to AWS EKS

The application is designed to be deployed to an AWS EKS cluster. The deployment process typically involves:
1.  Building the Docker image using the `Dockerfile`.
2.  Pushing the Docker image to AWS ECR.
3.  Using Ansible (as defined in `ansible/playbook.yml` and related roles) to apply the Kubernetes configurations (`deployment.yaml`) to the EKS cluster. This creates the necessary deployments and services to run the application and expose it.

The `deployment.yaml` file specifies:
*   A Kubernetes `Deployment` to manage the application pods, using the image from ECR.
*   A Kubernetes `Service` of type `LoadBalancer` to expose the application to the internet.

## Project Structure Highlights

*   `src/`: Contains the core Python source code for data processing, feature engineering, model training, and evaluation.
*   `flask_app/`: Contains the Flask application for serving the model.
*   `dvc.yaml`: Defines the DVC pipeline stages.
*   `params.yaml`: Contains parameters for the DVC pipeline.
*   `Dockerfile`: Defines how to build the application's Docker image.
*   `deployment.yaml`: Kubernetes manifest for deploying the application.
*   `ansible/`: Contains Ansible playbooks and roles for EKS deployment.
*   `requirements.txt`: Lists Python dependencies.
*   `Makefile`: Provides helper commands for development.

