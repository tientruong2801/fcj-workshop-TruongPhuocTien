---
title : "Prerequiste"
date : 2024-01-01 
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

# Prerequisites

Before starting this workshop, ensure you have the following tools installed and configured.

## Required Accounts & Permissions

### AWS Account
- **AWS Account** with administrative privileges or permissions for the following services:
  - VPC, EC2, Subnets, Route Tables, Internet Gateway
  - RDS (Aurora PostgreSQL Serverless v2)
  - ECS (Fargate, Clusters, Task Definitions, Services)
  - ECR (Repositories)
  - Lambda (Functions, Layers, Permissions)
  - SQS (Queues)
  - EventBridge (Rules, Schedules, Targets)
  - API Gateway (REST APIs)
  - Bedrock (Model access: `amazon.titan-embed-text-v2:0`)
  - IAM (Roles, Policies)
  - CloudWatch (Log Groups, Metrics)
  - CloudFormation (Stacks)

> **Tip:** Use an IAM user with `AdministratorAccess` for the workshop, or ensure your role has the permissions listed above.

### External API Keys (for RAG)
- **Groq API Key** — Get from [console.groq.com](https://console.groq.com/) (Free tier available)
- **Google Gemini API Key** — Get from [aistudio.google.com](https://aistudio.google.com/) (Free tier available)

## Mandatory Tools

### 1. AWS CLI v2
```bash
# macOS
brew install awscli

# Linux
curl "[https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip](https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip)" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

# Windows
msiexec.exe /i [https://awscli.amazonaws.com/AWSCLIV2.msi](https://awscli.amazonaws.com/AWSCLIV2.msi)

# Verify
aws --version
# Should output: aws-cli/2.x.x
```

**Configure AWS CLI:**
```bash
aws configure
# Enter: AWS Access Key ID, Secret Access Key, Region (e.g., ap-southeast-2), Output format (json)
```

### 2. Docker & Docker Compose
```bash
# macOS (Docker Desktop)
brew install --cask docker

# Linux
curl -fsSL [https://get.docker.com](https://get.docker.com) | sh
sudo usermod -aG docker $USER
# Log out and log back in

# Docker Compose (usually included with Docker Desktop)
# Standalone Linux:
sudo curl -L "[https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname](https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname) -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Verify
docker --version
docker compose version
```

### 3. Python 3.10+
```bash
# macOS
brew install python@3.11

# Linux (Ubuntu/Debian)
sudo apt update && sudo apt install python3.11 python3.11-venv python3.11-dev

# Windows
# Download from python.org

# Verify
python3 --version
# Should be 3.10.x or higher
```

### 4. Git
```bash
# macOS
brew install git

# Linux
sudo apt install git

# Windows
# Download from git-scm.com

# Verify
git --version
```

### 5. Code Editor (Recommended: VS Code)
```bash
# macOS
brew install --cask visual-studio-code

# Linux
# Download from code.visualstudio.com

# Recommended Extensions:
# - Docker
# - Python
# - AWS Toolkit
# - YAML
```

## Project Setup

### Clone Repository
```bash
git clone <your-repo-url> AWS-Projects
cd AWS-Projects
```

### Python Virtual Environment
```bash
python3 -m venv venv
source venv/bin/activate  # Linux/macOS
# venv\Scripts\activate   # Windows

pip install --upgrade pip
pip install -r requirements.txt
```

### Environment Variables
Copy the example file and fill in your values:
```bash
cp .env.example .env
```

Edit `.env` with your credentials:
```env
# Database (Aurora - fill in after setup on AWS)
DB_NAME=newsrag
DB_USER=postgres
DB_PASSWORD=your_secure_password
DB_HOST=your-aurora-endpoint.cluster-xyz.ap-southeast-2.rds.amazonaws.com
DB_PORT=5432

# Qdrant (for local dev only)
QDRANT_HOST=localhost
QDRANT_PORT=6333
QDRANT_COLLECTION_NAME=news_chunks
QDRANT_API_KEY=

# Kafka (for local dev only)
KAFKA_BOOTSTRAP_SERVERS=localhost:9092
KAFKA_TOPIC_NEWS=news_raw

# Embedding Model (local dev)
EMBEDDING_MODEL=BAAI/bge-small-en-v1.5
EMBEDDING_SIZE=384

# LLM APIs (Get from respective consoles)
GROQ_API_KEY=gsk_xxxxxxxxxxxxxxxxxxxx
GEMINI_API_KEY=AIza_xxxxxxxxxxxxxxxxxxxx

# AWS
AWS_REGION=ap-southeast-2
```

> **Security:** Never commit `.env` to git. It is already included in `.gitignore`.

## Verify Setup

Run the verification script:
```bash
make verify
```

Or manually check individual tools:
```bash
aws sts get-caller-identity  # Should display your AWS account
docker run hello-world       # Should print "Hello from Docker!"
python3 -c "import scrapy; print('Scrapy OK')"
```

## AWS Region

This workshop uses **ap-southeast-2 (Sydney)** by default. To change it:
1. Update `AWS_REGION` in `.env`
2. Ensure the Bedrock model `amazon.titan-embed-text-v2:0` is available in your region (check [Bedrock regions](https://docs.aws.amazon.com/bedrock/latest/userguide/models-regions.html))

## Bedrock Model Access

Enable model access in the AWS Console:
1. Go to **Amazon Bedrock** → **Model access**
2. Click **Manage model access**
3. Enable **Amazon Titan Embeddings G1 - Text v2** (`amazon.titan-embed-text-v2:0`)
4. Wait for the status to show "Access granted"

---

**Next:** [Infrastructure Setup on AWS Console](5.3-Infrastructure/)