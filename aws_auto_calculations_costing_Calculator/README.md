# ☁️ AWS Cost Estimator

Full-stack app: FastAPI backend + React frontend.
Estimate AWS infrastructure costs and get AI optimization tips.

---

## 📁 Project Structure

```
aws-cost-estimator/
├── backend/
│   ├── main.py            ← FastAPI app (all pricing logic)
│   └── requirements.txt
└── frontend/
    ├── package.json
    ├── public/index.html
    └── src/
        ├── index.js
        └── App.jsx        ← React UI
```

---

## 🚀 Run Locally

### 1. Backend (FastAPI)
```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```
- API runs at:  http://localhost:8000
- Swagger docs: http://localhost:8000/docs

### 2. Frontend (React)
```bash
cd frontend
npm install
npm start
```
- UI runs at: http://localhost:3000

---

## 🌐 Expose to Public URL (for Demo)

### Option A — ngrok (fastest, 1 command)
```bash
# Install: https://ngrok.com/download
ngrok http 3000
# → You get: https://abc123.ngrok.io  ← share this URL
```

### Option B — Railway (permanent, free tier)
```bash
# 1. Push to GitHub
# 2. Go to https://railway.app
# 3. New Project → Deploy from GitHub
# 4. Set root dir = backend, start cmd = uvicorn main:app --host 0.0.0.0 --port $PORT
# 5. Deploy frontend separately or use Vercel (below)
```

### Option C — Vercel (frontend) + Railway (backend)
```bash
# Frontend → Vercel
npm install -g vercel
cd frontend
vercel --prod

# Update API URL in App.jsx:
# const API = "https://your-railway-backend.up.railway.app";
```

---

## 🔌 API Endpoints

| Method | Endpoint           | Description                  |
|--------|--------------------|------------------------------|
| GET    | /                  | Health check                 |
| GET    | /docs              | Swagger UI                   |
| GET    | /services/ec2-types| List EC2 instance types       |
| GET    | /services/rds-types| List RDS instance types       |
| POST   | /estimate          | Calculate cost + get tips    |

### Sample POST /estimate
```json
{
  "ec2_instances": [
    { "instance_type": "t3.medium", "count": 2, "os": "linux", "usage_hours": 730 }
  ],
  "rds_instances": [
    { "instance_type": "db.t3.medium", "engine": "mysql", "multi_az": true, "storage_gb": 100 }
  ],
  "s3_config": {
    "storage_gb": 500, "put_requests": 100000, "get_requests": 1000000, "transfer_out_gb": 50
  },
  "lambda_config": {
    "requests_per_month": 5000000, "avg_duration_ms": 300, "memory_mb": 256
  }
}
```

---

## ✅ Features
- EC2, RDS, Lambda, S3, EKS, EBS, ELB, CloudFront pricing
- Visual pie + bar charts
- Per-service cost breakdown
- Optimization tips with estimated savings
- Annual cost projection
- REST API (Swagger auto-docs)

## 🗺️ Roadmap
- [ ] Azure pricing support
- [ ] GCP pricing support  
- [ ] Export to PDF/CSV
- [ ] Save/load configurations
- [ ] AWS Cost Explorer API integration (real prices)
