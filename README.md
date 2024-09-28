# 🐦 Twoge - A Simple Twitter Alternative

Welcome to **Twoge**! This is a simple Twitter-like application where users can create and post tweets. Follow the instructions below to get started, whether you're deploying locally or on a cloud platform using Kubernetes or AWS EKS!

---

## 🏗️ Architecture

### **Local Deployment (Docker + PostgreSQL)**

```plaintext
+----------------------+          +-----------------------+
|    Web Browser       |          |    PostgreSQL DB      |
|   (localhost:5000)   |  <--->   |    (Port: 5432)        |
+----------------------+          +-----------------------+
            |                             |
            v                             ^
+-----------------------------------------+
|               Flask Backend             |
|    (Python, SQLAlchemy, Psycopg2)       |
+-----------------------------------------+
```

### **Minikube + Kubernetes Deployment**

```plaintext
+--------------------------+      +----------------------+
|   Web Browser (localhost) |      |   Minikube Cluster   |
+--------------------------+      +----------------------+
            |                               |
            v                               v
+-------------------------------------------------------+
|                Kubernetes Cluster (Minikube)          |
|  +-------------------+       +-------------------+    |
|  |    Flask Pod      |       |   PostgreSQL Pod   |    |
|  |  (Flask Backend)  | <----> |  (PostgreSQL DB)  |    |
+-------------------------------------------------------+
```

- **Minikube** simulates a local Kubernetes environment where the Flask backend and PostgreSQL database are deployed in separate pods, managed by Kubernetes.

### **AWS EKS Deployment**

```plaintext
+--------------------------+      +----------------------+
|   Web Browser (public URL) |     |   AWS EKS Cluster    |
+--------------------------+      +----------------------+
            |                               |
            v                               v
+-------------------------------------------------------+
|                Kubernetes Cluster (AWS EKS)           |
|  +-------------------+       +-------------------+    |
|  |    Flask Pod      |       |   PostgreSQL Pod   |    |
|  |  (Flask Backend)  | <----> |  (PostgreSQL DB)  |    |
|                       |       |                   |    |
+-------------------------------------------------------+
            ^                                ^
            |                                |
   +-------------------+            +-------------------+
   |    AWS Load       |            |  AWS RDS (Optional)|
   |    Balancer       |            |    (PostgreSQL DB) |
   +-------------------+            +-------------------+
```

- **AWS EKS (Elastic Kubernetes Service)** allows you to deploy Twoge on a managed Kubernetes cluster, where you can scale the app seamlessly.
- PostgreSQL can either run in a pod or use **AWS RDS** for a managed database service.

---

## 🚀 Getting Started

### Step-by-Step Instructions

Follow these steps to set up Twoge on your local machine or on a Kubernetes cluster.

1. **Clone the Repository** 🖥️:
   ```bash
   git clone https://github.com/nekablair/twoge-assessment4.git
   cd twoge
   ```

2. **Create and Activate a Virtual Environment** 🐍:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

   > 💡 On Windows, use `venv\Scripts\activate` to activate the virtual environment.

3. **Install Dependencies** 📦:
   Install all required packages using `pip`:
   ```bash
   pip install -r requirements.txt
   ```

4. **Set Up PostgreSQL Database** 🗄️:
   Create a PostgreSQL database for Twoge:
   ```sql
   CREATE DATABASE twoge_db;
   ```

5. **Configure Environment Variables** 🔧:
   Set the `DATABASE_URL` environment variable:
   ```bash
   export DATABASE_URL="postgresql://postgres:yourpassword@localhost:5432/twoge_db"
   ```

6. **Run the Application Locally** ⚙️:
   Start the Flask app:
   ```bash
   python app.py
   ```

7. **Access Twoge in Your Browser** 🌐:
   Open your browser and navigate to:
   ```
   http://localhost:5000
   ```

---

## 📦 Deploying with Minikube and Kubernetes

### Install Minikube:
1. Follow the [Minikube installation guide](https://minikube.sigs.k8s.io/docs/start/).
2. Start Minikube:
   ```bash
   minikube start
   ```

### Kubernetes Configuration:
1. Create a Kubernetes deployment for both the Flask app and PostgreSQL:
   ```bash
   kubectl apply -f k8s/deployment.yaml
   kubectl apply -f k8s/service.yaml
   ```

2. Expose the Flask application on a port to access it from your browser:
   ```bash
   minikube service flask-service
   ```

3. Access Twoge using the Minikube IP provided.

---

## ☁️ Deploying with AWS EKS

### Step 1: Create an EKS Cluster
1. Set up an AWS EKS Cluster following [AWS documentation](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html).
2. Ensure you have kubectl configured to work with your EKS cluster:
   ```bash
   aws eks update-kubeconfig --name your-cluster-name --region your-region
   ```

### Step 2: Deploy Application on EKS
1. Apply the Kubernetes manifests for the Flask app and PostgreSQL database:
   ```bash
   kubectl apply -f k8s/deployment.yaml
   kubectl apply -f k8s/service.yaml
   ```

2. If using **AWS RDS** for PostgreSQL, configure the `DATABASE_URL` in your application to use the RDS instance.

3. Access the application through the **AWS Load Balancer** created for the Flask service.

---

## 🛠️ Database Schema

Twoge's database consists of a single table that stores information about each tweet. The table includes the following attributes:

- `date_posted`: The date and time when the tweet was posted.
- `author`: The user who posted the tweet.
- `title`: The title of the tweet.
- `content`: The content of the tweet.

---

## 📷 Screenshots

![Twoge Screenshot1](twoge-minikube.PNG)
![Twoge Screenshot2](twoge-minikube2.PNG)
![Twoge Screenshot3](twoge-minikube3.PNG)
![Twoge Screenshot4](twoge-minikube4.PNG)
![Twoge Screenshot5](twoge-minikube5.PNG)

---

## 🎥 Video Walkthrough


```markdown
![Twoge Walkthrough](assessment4-twoge-recording-19september24.mp4)
```

---

## 📝 Contributing

We welcome contributions! Please fork the repository and submit pull requests for review.

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

### 📬 Get in Touch

If you have any questions or run into any issues, feel free to open an issue or reach out.
