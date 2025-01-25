# MLOps Cheatsheet
 ChatGPT based fyi  
 
<img width="1420" alt="Screenshot 2025-01-25 at 18 49 53" src="https://github.com/user-attachments/assets/19f11882-57ba-42d1-a2f8-fd069df39b95" />

 
## 🚀 MLOps Nedir?
MLOps (Machine Learning Operations), makine öğrenimi modellerinin üretime alınması, yönetilmesi ve izlenmesi süreçlerini kapsayan bir disiplindir. Yazılım mühendisliği (DevOps) ve veri biliminin kesişim noktasında yer alır.

### **MLOps Süreç Adımları:**
1. **Veri Toplama:** API'ler, veri tabanları, dosyalar.
2. **Veri İşleme ve Hazırlama:** Pandas, NumPy, Feature Engineering.
3. **Model Geliştirme:** Scikit-learn, TensorFlow, PyTorch.
4. **Model Versiyonlama:** DVC, MLflow.
5. **Model Deploy:** FastAPI, Flask, AWS, Azure.
6. **Sürekli Entegrasyon & Dağıtım (CI/CD):** GitHub Actions, Jenkins.
7. **İzleme ve Geri Bildirim:** Prometheus, Grafana.

---

## 🛠 CI/CD Pipeline Nedir?
**Continuous Integration (CI):** Yazılımın düzenli olarak birleştirilmesi ve test edilmesi.

**Continuous Deployment/Delivery (CD):** Test edilen yazılımın otomatik olarak dağıtılması.

### **CI/CD Süreci:**
1. Kod Push (GitHub, GitLab).
2. Testlerin Çalıştırılması.
3. Docker Image Build edilmesi.
4. Image'in Docker Hub veya ECR'ye push edilmesi.
5. Deployment (AWS EC2, Kubernetes, Heroku).

### **GitHub Actions Örneği**

```yaml
name: CI/CD for ML Model
on:
  push:
    branches:
      - main

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.9'
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run tests
        run: pytest
  deploy:
    needs: build-and-test
    runs-on: ubuntu-latest
    steps:
      - name: Build Docker Image
        run: docker build -t my-ml-app .
      - name: Push Docker Image
        run: docker push mydockerhubuser/my-ml-app
```

---

## 🐳 Docker ile Çalışma
Docker, uygulamaları bağımsız çalıştırmak için kullanılan bir konteyner platformudur.

### **Temel Komutlar**

```bash
# Docker image oluşturma
docker build -t my-ml-app .

# Docker container çalıştırma
docker run -d -p 8000:8000 my-ml-app

# Docker image push etme
docker push mydockerhubuser/my-ml-app

# Çalışan container'ları listeleme
docker ps

# Container durdurma
docker stop container_id
```

### **Dockerfile Örneği**

```dockerfile
FROM python:3.9
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

---

## ⚡ FastAPI ile REST API Geliştirme

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def root():
    return {"message": "Merhaba MLOps"}
```

### **Çalıştırma:**
```bash
uvicorn main:app --reload
```

### **Test Etme:**
- Swagger UI: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## ☁ AWS EC2'ye Deployment

**AWS EC2 Üzerinde Docker Kullanımı:**

```bash
# EC2'ye SSH bağlantısı
ssh -i my-key.pem ec2-user@ec2-instance-ip

# Docker kurulumu
sudo apt update
sudo apt install docker.io -y

# Docker Hub'dan image çekme
sudo docker pull mydockerhubuser/my-ml-app

# Container çalıştırma
sudo docker run -d -p 80:8000 mydockerhubuser/my-ml-app
```

---

## 📈 Model İzleme ve Yönetimi

**MLflow Kullanımı:**
```bash
# MLflow başlatma
mlflow server --backend-store-uri sqlite:///mlflow.db --default-artifact-root ./mlruns --host 0.0.0.0 --port 5000
```

**Kod Örneği:**
```python
import mlflow

mlflow.log_param("learning_rate", 0.01)
mlflow.log_metric("accuracy", 0.95)
mlflow.log_artifact("model.pkl")
```

**UI:** [http://localhost:5000](http://localhost:5000)

---

## 📋 MLOps'da Kullanılan Araçlar

| Kategori          | Araçlar                                    |
|------------------|--------------------------------------------|
| Model Geliştirme  | TensorFlow, PyTorch, Scikit-learn          |
| Model Versiyonlama | MLflow, DVC                               |
| Sürekli Entegrasyon | GitHub Actions, Jenkins                   |
| Konteynerleştirme | Docker, Kubernetes                        |
| Dağıtım            | AWS SageMaker, Azure ML, GCP AI Platform  |
| İzleme            | Prometheus, Grafana                        |

---

Ekleme yapmak isterseniz pr atmanız yeterli, byee
