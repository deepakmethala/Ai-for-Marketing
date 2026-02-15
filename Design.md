#  RetailPulse AI – System Design Document

## 1. System Overview

RetailPulse AI is a cloud-based web application that provides:

- Sales analytics
- Demand forecasting (30/60/90 days)
- Pricing optimization
- Inventory risk analysis
- AI-powered business recommendations

Users upload sales and inventory data. The system processes it using ML models and displays insights through dashboards and an AI Copilot.

---

## 2. High-Level Architecture

User (Browser)  
↓  
Frontend (Next.js / React)  
↓  
Backend API (FastAPI)  
↓  
PostgreSQL + Redis  
↓  
ML Services (Forecasting, Pricing, Risk Models)  
↓  
Dashboard + AI Copilot  

---

## 3. Core Components

### 3.1 Frontend
- User login & authentication
- Dashboard with charts
- SKU analytics view
- Forecast visualization
- Pricing simulation UI
- AI Copilot chat interface

**Tech:** Next.js, React, Tailwind CSS, Chart.js/Recharts

---

### 3.2 Backend
- Authentication (JWT)
- Data upload APIs
- Business logic
- ML model execution
- Alert generation

**Tech:** FastAPI (Python), REST APIs

---

### 3.3 Database

**PostgreSQL Tables:**
- Users
- Products
- Sales
- Inventory
- Forecast
- SKU_Scores
- Alerts

**Redis:**
- Cache dashboard data
- Improve API performance

---

### 3.4 AI / ML Layer

**1️ Demand Forecasting**
- Predicts 30/60/90 day sales
- Uses Prophet / LSTM
- Provides confidence intervals

**2️ Pricing Engine**
- Estimates price elasticity
- Simulates revenue impact
- Suggests optimal price range

**3️ Inventory & Risk Engine**
- Calculates days-of-cover
- Detects slow-moving products
- Identifies sales drops & margin erosion

**4️ AI Copilot**
- Converts analytics into simple business explanations
- Answers user queries using internal data

---

## 4. Data Flow

1. User uploads sales & inventory data  
2. System validates and preprocesses data  
3. ML models generate forecasts & risk scores  
4. Results stored in database  
5. Dashboard & Copilot display insights  

---

## 5. Key APIs

### Authentication
- POST /register
- POST /login

### Data Upload
- POST /upload-sales
- POST /upload-inventory
- POST /upload-products

### Analytics
- GET /dashboard-summary
- GET /forecast/{sku_id}?days=90
- POST /pricing/simulate
- GET /alerts
- POST /copilot/query

---

## 6. Security

- HTTPS communication
- JWT authentication
- Encrypted passwords (bcrypt)
- Role-based access control
- Input validation

---

## 7. Deployment

- Frontend: Vercel / AWS
- Backend: AWS EC2 / Cloud Run
- Database: AWS RDS (PostgreSQL)
- ML Services: Docker containers
- CI/CD: GitHub Actions

---

## 8. Future Scope

- Real-time marketplace integration
- Dynamic pricing automation
- Multi-store analytics
- Mobile application
