# 🔐 Environment Variables in Test Automation (CI/CD)

## 🎯 Purpose
Environment variables are used to:
- Avoid hardcoding values (URLs, credentials)
- Secure sensitive data
- Enable multi-environment execution (QA, Staging, Prod)
- Integrate seamlessly with CI/CD pipelines

---

# 🧩 Why Use Environment Variables?

✅ No code changes for different environments  
✅ Secure handling of secrets  
✅ Easy CI/CD integration  
✅ Scalable framework design  

---

# 🧪 Example (Pytest)

```python
import os
import pytest

@pytest.fixture(scope="session")
def base_url():
    url = os.getenv("BASE_URL")
    if not url:
        raise ValueError("BASE_URL not set")
    return url
```

---

# 🏠 LOCAL SETUP APPROACHES

## ✅ Approach 1: Direct Environment Variable (Terminal)

### Set variable:
```bash
# Linux/Mac
export BASE_URL=https://qa.example.com

# Windows
set BASE_URL=https://qa.example.com
```

### Run tests:
```bash
pytest
```

✔ Quick and simple  
❌ Not reusable across sessions  

---

## ✅ Approach 2: Using `.env` File (Best for Local Dev)

### Step 1: Create `.env`
```env
BASE_URL=https://qa.example.com
API_KEY=secret123
```

### Step 2: Install dotenv
```bash
pip install python-dotenv
```

### Step 3: Load in code
```python
from dotenv import load_dotenv
import os

load_dotenv()
```

### Step 4: Add to `.gitignore`
```
.env
```

✔ Reusable  
✔ Clean setup  
✔ Keeps secrets out of Git  

---

# 🚀 CI/CD SETUP (JENKINS)

## ❌ Wrong Approach
- Uploading `.env` file directly to Jenkins
- Committing `.env` to Git

---

## ✅ Approach 1: Jenkins Environment Variables (Direct)

```groovy
pipeline {
    agent any

    environment {
        BASE_URL = "https://qa.example.com"
    }

    stages {
        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }
    }
}
```

✔ Simple  
❌ Not secure for sensitive data  

---

## 🔐 Approach 2: Jenkins Credentials (Recommended)

### Step 1: Add Credential
- Manage Jenkins → Credentials
- Kind: Secret Text
- ID: base-url

### Step 2: Use in Pipeline
```groovy
pipeline {
    agent any

    environment {
        BASE_URL = credentials('base-url')
    }

    stages {
        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }
    }
}
```

✔ Secure  
✔ Not exposed in logs  

---

## 📁 Approach 3: Jenkins Secret File (.env style)

```groovy
pipeline {
    agent any

    stages {
        stage('Load Env') {
            steps {
                withCredentials([file(credentialsId: 'env-file', variable: 'ENV_FILE')]) {
                    sh '''
                        set -a
                        source $ENV_FILE
                        set +a
                        pytest
                    '''
                }
            }
        }
    }
}
```

✔ Supports `.env` format  
✔ Secure  

---

# 🔄 MULTI-ENVIRONMENT SUPPORT

```python
ENV_URLS = {
    "qa": "https://qa.example.com",
    "staging": "https://staging.example.com",
    "prod": "https://prod.example.com"
}

def get_base_url():
    import os
    env = os.getenv("ENV", "qa")
    return ENV_URLS[env]
```

Run:
```bash
ENV=staging pytest
```

---

# ⚠️ Common Mistakes

❌ Hardcoding values  
❌ Committing `.env` to Git  
❌ Printing secrets in logs  
❌ Not validating env variables  

---

# 🧠 Interview Answer (Short)

Environment variables are used in test automation to externalize configuration such as URLs, credentials, and execution parameters. They allow the same test suite to run across multiple environments without code changes. In CI/CD tools like Jenkins, environment variables are injected at runtime, ensuring secure and flexible execution.

---

# 🏁 Best Practice Summary

| Use Case        | Recommended Approach        |
|----------------|---------------------------|
| Local Dev      | `.env` + python-dotenv     |
| CI/CD Secure   | Jenkins Credentials        |
| Simple CI/CD   | Environment block          |
| Multi-env      | ENV + mapping logic        |
