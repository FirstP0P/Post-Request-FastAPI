### **README (Updated with Streamlit & Algorithm Info)**

# Insurance Premium Prediction 🚀

This project is an **end-to-end Machine Learning application** that predicts insurance premiums based on user input (age, BMI, smoking status, region, etc.).
It integrates a trained **Random Forest Regressor model** with a **FastAPI backend**, a **Streamlit frontend**, and is fully containerized using Docker for deployment on AWS EC2.

---

## 📂 Project Structure

```
insurance-premium-prediction/
│── main.py                 # Entry point for starting backend
│── app.py                  # FastAPI application (model serving API)
│── frontend.py              # Streamlit app (frontend UI)
│── model.pkl               # Pre-trained Random Forest Regressor model
│── insurance.csv           # Dataset used for training
│── patients.json           # Example input JSON
│── fastapi_ml_model.ipynb  # Notebook for experimentation & training
│── requirements.txt        # Python dependencies
│── .gitignore
│── Step_1_Creating_model_pkl.png
│── Step_2a_Creating_endpoint_API_Endpoint.png
│── Step_2b_Input_and_Output.png
│── Improved API.png
```

---

## ⚙️ Workflow Explanation

### **Step 1 – Model Training**

* Dataset: `insurance.csv`
* Algorithm: **Random Forest Regressor** (trained in `fastapi_ml_model.ipynb`)
* Features: age, sex, BMI, children, smoker, region.
* Target: insurance premium (`charges`).
* Model saved as `model.pkl` for inference.

### **Step 2 – Backend (FastAPI)**

* `app.py` loads `model.pkl` and provides `/predict` API endpoint.
* Workflow:

  1. Receive JSON input.
  2. Preprocess input.
  3. Call Random Forest Regressor model.
  4. Return premium prediction.

### **Step 3 – Frontend (Streamlit)**

* `frontend.py` is a **Streamlit app**.
* It provides an interactive web interface where users can input values (age, BMI, smoking status, etc.).
* The Streamlit app sends data to the FastAPI backend and displays predictions in real-time.

### **Step 4 – Dockerization**

* Dockerfile builds a containerized version of the app:

  * Installs dependencies from `requirements.txt`.
  * Runs FastAPI and Streamlit inside the container.
* Commands:

  ```bash
  docker build -t insurance-premium-prediction .
  docker run -p 8000:8000 insurance-premium-prediction
  ```

### **Step 5 – AWS Deployment**

* Image uploaded to **DockerHub**.
* EC2 Ubuntu instance pulls image and runs container.
* Accessible at:

  ```
  http://<EC2-Public-IP>:8000/docs   (FastAPI)
  http://<EC2-Public-IP>:8501        (Streamlit)
  ```

---

## 🧩 How Code Works Together

* **frontend.py (Streamlit)** → User inputs data → sends request to FastAPI backend.
* **app.py (FastAPI)** → Receives request → uses **Random Forest Regressor model (`model.pkl`)** → returns prediction.
* **Streamlit UI** updates with predicted premium.

Flow: **Streamlit → FastAPI → Random Forest Regressor model → Prediction → Streamlit Output**

---

## ▶️ Run Locally

1. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```
2. Start FastAPI backend:

   ```bash
   uvicorn app:app --reload
   ```

   Available at `http://127.0.0.1:8000/docs`
3. Start Streamlit frontend:

   ```bash
   streamlit run frontend.py
   ```

   Available at `http://localhost:8501`

---

## ▶️ Run with Docker

1. Build Docker image:

   ```bash
   docker build -t insurance-premium-prediction .
   ```
2. Run container (FastAPI + Streamlit):

   ```bash
   docker run -p 8000:8000 -p 8501:8501 insurance-premium-prediction
   ```
3. Access:

   * API: `http://localhost:8000/docs`
   * UI: `http://localhost:8501`

---

## ▶️ Run on AWS EC2

1. Launch Ubuntu EC2 instance and install Docker:

   ```bash
   sudo apt update
   sudo apt install docker.io -y
   ```
2. Pull image:

   ```bash
   docker pull <your-dockerhub-username>/insurance-premium-prediction
   ```
3. Run container:

   ```bash
   docker run -d -p 8000:8000 -p 8501:8501 <your-dockerhub-username>/insurance-premium-prediction
   ```
4. Access:

   * `http://<EC2-Public-IP>:8000/docs`
   * `http://<EC2-Public-IP>:8501`

---

## ✅ Conclusion

This project demonstrates a **complete ML pipeline**:

* **Random Forest Regressor model** for premium prediction.
* **FastAPI backend** for model serving.
* **Streamlit frontend** for interactive UI.
* **Docker** for containerization.
* **AWS EC2** for cloud deployment.

---
