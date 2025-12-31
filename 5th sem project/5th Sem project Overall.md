# **3-Month Roadmap for Yetinel SIEM**

### **Month 1: Foundations & Core Backend**

**Goal:** Get the ingestion server running and basic agents sending data.
	
| Week | Focus                     | Tasks / Deliverables                                                                                                                                         |
| ---- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1    | Rust & Axum Setup         | - Learn Axum basics & async Rust  <br>- Scaffold Yetinel ingestion server  <br>- Setup MongoDB                                                               |
| 2    | Core Ingestion            | - Implement `/ingest` API  <br>- JSON log parsing & validation  <br>- Insert logs into MongoDB  <br>- Simple `/heartbeat` route for agents                   |
| 3    | Security & API Keys       | - Add API key auth for agents  <br>- Validate incoming requests  <br>- Rate limiting & basic error handling                                                  |
| 4    | Python Analyzer Prototype | - Start Python module to read logs from MongoDB  <br>- Apply simple rules (e.g., failed login alerts)  <br>- Store analysis results in a separate collection |

---

### **Month 2: Agents & Analysis Layer**

**Goal:** Build multi-language agents and enhance analysis logic.

|Week|Focus|Tasks / Deliverables|
|---|---|---|
|5|Node.js Agent|- Build Node.js package for web apps  <br>- Send HTTP POST logs to `/ingest`  <br>- Add heartbeat & error logging|
|6|Python Agent|- Build Python package for backend apps  <br>- Collect logs/events, send to `/ingest`  <br>- Handle retries on failures|
|7|Analyzer Expansion|- Add rule-based engine for web attacks (XSS, SQLi attempts, brute force)  <br>- Start basic alert scoring system|
|8|Batch Processing|- Implement batch ingestion & processing  <br>- Optimize MongoDB queries  <br>- Start simple metrics aggregation (counts, trends)|

---

### **Month 3: Dashboard & Final Polish**

**Goal:** Make Yetinel fully visual, interactive, and deployable.

|Week|Focus|Tasks / Deliverables|
|---|---|---|
|9|React Dashboard Setup|- Scaffold React app  <br>- Connect to backend API  <br>- Show log streams & basic metrics|
|10|Visualization & Analytics|- Add charts (log trends, top attack vectors)  <br>- Add filters and search capabilities  <br>- Live updates via WebSockets or polling|
|11|Alerts & Notifications|- Highlight security alerts  <br>- Email/Slack notifications (optional)  <br>- Fine-tune scoring & rules|
|12|Testing & Deployment|- End-to-end testing (agents → Rust → Python → MongoDB → React)  <br>- Dockerize backend + agents  <br>- Prepare final demo & documentation|

---

### ✅ **Key Milestones**

1. **End of Month 1:** Ingestion server + MongoDB logging + basic Python analyzer
    
2. **End of Month 2:** Node & Python agents operational + basic analysis engine
    
3. **End of Month 3:** Dashboard live, alerts working, ready for demo or deployment
    

---

### 💡 **Extra Tips**

- Use **GitHub repo with branches**: `backend`, `frontend`, `agents`, `analyzer`
    
- Document everything in **Markdown/Obsidian** for future reference
    
- Keep **unit tests** for ingestion & analysis — saves headaches later
    
- Start **simple**; you can expand features after the core is stable