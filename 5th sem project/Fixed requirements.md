
---

# **Yetinel V1 – Final Requirements & Features**

## **Goal of V1**

Build a **working, secure, self-hosted SIEM MVP** that:

- Collects logs reliably
    
- Normalizes & analyzes them
    
- Generates alerts
    
- Visualizes everything in a clean dashboard
    

No ML. No dark web. No overengineering.

---

## **1. Core Architecture (Final)**

✔ **Two logical servers**.

- **Rust Ingestion Servers** (performance & security)
    
- **Python Analytics Servers** (flexibility & rules)
    
- MongoDB
    
- React Dashboard
    
- Docker Compose (single-node)
    

---

## **2. Log Ingestion Service (Rust)**

**Purpose:** Fast, secure entry point

### **Must-have**

- HTTP REST API (Axum) 
    
- JSON log ingestion
    
- API key / agent token authentication
    
- Rate limiting (per agent)
    
- Input validation & size limits
    
- Batch writes to MongoDB
    
- Structured logging (errors, access)
    
- Dockerized
    

### **Nice-to-have (still V1-acceptable)**

- Basic metrics endpoint (`/metrics`)
    
- Health check (`/health`)

❌ No Kafka  
❌ No gRPC  
❌ No clustering

---

## **3. Data Storage (MongoDB)**

**Collections**

- `raw_logs`
    
- `normalized_logs`
    
- `alerts`
    
- `agents`
    

### **Requirements**

- Indexed timestamps
    
- TTL support (optional)
    
- TLS connection
    
- Docker volume persistence
    

---

## **4. Analytics Engine (Python)**

**Purpose:** Turn logs into intelligence

### **Must-have**

- ECS-style normalization
    
- MITRE ATT&CK tagging
    
- Rule-based detections:
    
    - brute-force
        
    - suspicious IP
        
    - abnormal request rate
        
- Alert generation with severity
    
- REST API for frontend
    
- Dockerized
    

### **Rules Engine**

- YAML/JSON-based rules
    
- No ML
    
- Deterministic & explainable
    

---

## **5. Frontend Dashboard (React)**

**Purpose:** Visibility & usability

### **Must-have**

- Dark mode UI
    
- Login (basic auth / JWT)
    
- Log search & filters
    
- Alerts page
    
- Severity badges
    
- Timeline / charts
    
- Agent list & status
    

### **Tech**

- REST polling (no WebSockets yet)
    
- Recharts / Chart.js
    
- Responsive layout
    

---

## **6. Security (V1 Baseline)**

✔ TLS between services  
✔ Input sanitization  
✔ Docker network isolation  
✔ Secrets via env vars  
✔ Rate limiting  
✔ No public MongoDB exposure

---

## **7. DevOps & DX**

- Docker Compose (single command start)
    
- `.env` support
    
- Clear README
    
- Sample logs & agents
    
- Health checks for all services
    

---

## **8. Explicitly NOT in V1**

❌ Dark web monitoring  
❌ Threat intel feeds  
❌ ML / UEBA  
❌ Correlation across days  
❌ Multi-node scaling  
❌ Kubernetes

---

## **9. V1 Success Criteria (Ship Check)**

Yetinel V1 is **DONE** when:

- Logs arrive via API
    
- Logs are normalized
    
- Alerts are generated
    
- Dashboard shows data
    
- System survives basic abuse
    
- Demo looks legit
    

---

## **V2 Reserved Features**

- Dark web monitoring
    
- Threat intelligence feeds
    
- UEBA / ML
    
- Correlation engine
    
- Distributed ingestion
    
- Kubernetes
    
- SOC-grade dashboards