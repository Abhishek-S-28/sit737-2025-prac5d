# 737webapp – Microservice Deployment Guide 🚀

This project documents the steps taken to build, publish, and test the `737webapp` microservice using **Google Cloud Artifact Registry** and **Docker**.

---

## 📆 Project Overview

`737webapp` is a Dockerized microservice deployed via a private container registry in Google Cloud. The guide below walks through the complete publishing process.

---

## ✅ Prerequisites

- Docker installed locally
- Google Cloud SDK (`gcloud`) installed and configured
- Google Cloud project (ID: `my737webapp`)



---

## 🛠️ Step-by-Step Deployment Instructions

### 🔒 1. Create a Private Container Registry in Google Cloud

1. Go to **Google Cloud Console** → **Artifact Registry**
2. Click on **"Create Repository"**
3. Name: `sit737`
4. Format: `Docker`
5. Location: `us` (or your preferred region)
6. Visibility: **Private**

📁 This will store your container images securely.

---

### 🔐 2. Authenticate Docker with Artifact Registry

```bash
gcloud auth login
gcloud auth configure-docker us-docker.pkg.dev
```

This allows Docker to push/pull images from your private registry.

---

### 🏗️ 3. Build and Tag the Docker Image

```bash
docker build -t 737webapp .
docker tag 737webapp us-docker.pkg.dev/my737webapp/sit737/737webapp
```

Make sure your Dockerfile is in the project root.

---

### 📤 4. Push the Docker Image to Google Cloud

```bash
docker push us-docker.pkg.dev/my737webapp/sit737/737webapp
```

Your image is now published to the private registry and accessible via GCP services or future Docker pulls.

---

### 🧪 5. Test the Image Locally

If your container listens on port `3000`, map it like so:

```bash
docker run -d -p 8080:3000 us-docker.pkg.dev/my737webapp/sit737/737webapp
```

Then test:

```bash
curl http://localhost:8080
```

Or visit: [http://localhost:8080](http://localhost:8080)

---

## 📂 Artifact Registry Reference

- Repository: `sit737`
- Project ID: `my737webapp`
- Image URI: `us-docker.pkg.dev/my737webapp/sit737/737webapp`

---

## 📌 Useful Commands

```bash
# List images in the repository
gcloud artifacts docker images list us-docker.pkg.dev/my737webapp/sit737

# View image details
gcloud artifacts docker images describe us-docker.pkg.dev/my737webapp/sit737/737webapp

# Delete an image (optional)
gcloud artifacts docker images delete us-docker.pkg.dev/my737webapp/sit737/737webapp
```

---

## 👤 Author

Abhishek Srinivasan - S223750107

---

##

