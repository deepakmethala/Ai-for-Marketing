# Design Document

## Overview

SECTORWISE AI is an intelligent sector-based investment allocation engine designed for beginner retail investors. The system uses AI-driven multi-factor analysis to score stocks, allocate capital optimally, and simulate future scenarios with full transparency and explainability.

## Architecture

### High-Level Architecture

**Frontend → API Gateway → Lambda Functions → ML Services → Database**

### Components

#### 1. Frontend Layer (React.js + Tailwind CSS)
- Landing Page
- Risk Profile Form
- Sector Selection Interface
- Allocation Dashboard
- Stock Detail View
- Scenario Simulator Page
- Portfolio Breakdown Page

#### 2. API Layer (AWS API Gateway)
- RESTful API endpoints
- Rate limiting
- Request validation
- JWT token verification

#### 3. Backend Services (AWS Lambda)
- User management service
- Stock analysis service
- Scoring engine service
- Allocation engine service
- Prediction service
- Scenario simulation service

#### 4. ML/AI Layer
- Amazon SageMaker: ML model training and hosting
- Amazon Comprehend: Sentiment analysis
- Amazon Forecast: Time-series predictions
- Custom models: Random Forest, XGBoost, LSTM

#### 5. Data Layer
- Amazon RDS (PostgreSQL): Structured data (users, stocks, allocations, sectors)
- Amazon S3: Historical price data, model artifacts
- CloudWatch: Logs and monitoring

#### 6. Authentication Layer
- AWS Cognito: User authentication and authorization

### Data Flow

1. User inputs investment details → Frontend
2. Frontend sends request → API Gateway
3. API Gateway authenticates → AWS Cognito
4. Lambda function processes request
5. Stock analysis engine fetches data → RDS/S3
6. Scoring engine calculates scores
7. ML models generate predictions → SageMaker
8. Allocation engine distributes capital
9. Results returned → Frontend
10. Dashboard displays visualizations

### Technology Stack

**Frontend:**
- React.js
- Tailwind CSS
- Chart.js / Recharts
- Axios for API calls

**Backend:**
- Node.js / Python (Lambda functions)
- Express.js (if using EC2)

**Database:**
- PostgreSQL (Amazon RDS)
- Amazon S3 (object storage)

**ML/AI:**
- Python (scikit-learn, XGBoost, TensorFlow/Keras)
- Amazon SageMaker
- Amazon Comprehend
- Amazon Forecast

**Infrastructure:**
- AWS Amplify (frontend hosting)
- AWS Lambda (serverless compute)
- AWS API Gateway
- AWS EC2 (ML processing)
- AWS Cognito (authentication)
- AWS CloudWatch (monitoring)

## Design Decisions

### 1. Scoring Model Architecture

**Weighted Multi-Factor Model:**
```
Final Stock Score = 
  (0.40 × Fundamental Score) +
  (0.30 × Technical Score) +
  (0.20 × Sector Momentum Score) +
  (0.10 × Sentiment Score)
```

**Fundamental Score Breakdown:**
- ROE: 15%
- ROCE: 15%
- Revenue Growth: 15%
- Profit Growth: 15%
- Debt Ratio: 10%
- PEG: 10%
- Promoter Holding: 10%
- Free Cash Flow: 10%

**Rationale:** Prioritizes fundamental strength while incorporating technical and sentiment signals for comprehensive analysis.

### 2. Capital Allocation Strategy

**Formula:**
```
Allocation % = (Stock Score / Total Sector Score) × Investment Amount
```

**Risk-Based Adjustments:**
- Low Risk: Higher allocation to large cap, reduce volatility weighted stocks
- Medium Risk: Balanced distribution
- High Risk: Include midcaps, allow higher volatility weight

**Diversification Rules:**
- Max 40% in one stock
- Minimum 3 stocks per allocation
- Volatility cap based on risk profile

**Rationale:** Balances performance optimization with risk management and diversification.

### 3. Prediction Engine Design

**Three-Model Ensemble:**
1. Random Forest Regressor: Captures non-linear relationships
2. XGBoost: Handles feature interactions efficiently
3. LSTM: Captures time-series patterns

**Inputs:**
- Historical prices
- Technical indicators
- Fundamental score
- Sentiment score

**Outputs:**
- Expected return range (1Y)
- Best Case / Worst Case scenarios
- Probability distribution curve

**Rationale:** Ensemble approach reduces model bias and provides robust predictions.

### 4. Database Schema

**Tables:**

**Users**
- id (PK)
- risk_profile
- time_horizon
- created_at

**Stocks**
- ticker (PK)
- sector
- market_cap
- pe, roe, roce, debt_equity
- growth_rate
- volatility
- sentiment_score

**SectorData**
- sector_name (PK)
- growth_rate
- volatility
- momentum_score
- heat_index

**Allocations**
- id (PK)
- user_id (FK)
- stock_ticker (FK)
- allocation_amount
- expected_return
- risk_score

**Rationale:** Normalized schema for efficient queries and data integrity.

### 5. UI/UX Design Principles

**Visual Elements:**
- Clean fintech theme
- Dark & light mode support
- Glassmorphism cards
- Animated charts
- Responsive design

**User Experience:**
- Beginner-friendly tooltips
- Progressive disclosure of complexity
- Visual risk indicators
- Interactive scenario simulations

**Dashboard Components:**
- Allocation Pie Chart
- Risk Meter
- Sector Health Indicator
- Probability Distribution Chart
- Stock Comparison Table
- Heatmap of metrics
- Marriage Proposal Score (circular meter)

**Rationale:** Reduces cognitive load for beginner investors while maintaining professional appearance.

### 6. Security Architecture

- JWT tokens for stateless authentication
- AWS Cognito for user management
- Encrypted connections (TLS/SSL)
- Rate limiting to prevent abuse
- Input validation and sanitization
- No storage of sensitive financial credentials

**Rationale:** Multi-layered security approach following AWS best practices.

### 7. Scenario Simulation Design

**Three Scenarios:**
- Conservative: 25th percentile
- Expected: 50th percentile
- Aggressive: 75th percentile

**Risk Metrics:**
- Sharpe Ratio
- Max Drawdown
- Portfolio Volatility

**Rationale:** Provides realistic range of outcomes without guaranteeing returns.

## Advanced Features

### 1. Rebalancing Alerts
Monitor portfolio drift and suggest rebalancing when allocations deviate significantly.

### 2. Sector Rotation Detection
Identify sector momentum shifts and alert users to potential opportunities.

### 3. Portfolio Drift Analysis
Track how actual portfolio performance deviates from expected allocation.

### 4. Risk Tolerance Recalibration
Suggest risk profile adjustments based on user behavior and market conditions.

### 5. Institutional Buying Tracker
Monitor institutional investor activity as a sentiment signal.

### 6. Market Cycle Indicator
Identify current market phase (accumulation, markup, distribution, markdown).

### 7. AI Explainability Panel
Provide detailed breakdown of why each stock was scored and allocated as it was.

## Deployment Architecture

**Development Environment:**
- Local development with Docker containers
- Mock data for testing

**Staging Environment:**
- AWS infrastructure mirror
- Synthetic data for testing

**Production Environment:**
- AWS Amplify: Frontend hosting with CDN
- AWS Lambda: Auto-scaling backend services
- Amazon RDS: Multi-AZ deployment for high availability
- Amazon S3: Versioned storage for historical data
- CloudWatch: Real-time monitoring and alerting

## Future Considerations

- Multi-sector portfolio allocation
- International market support
- Real-time price updates via WebSocket
- Mobile native apps (iOS/Android)
- Social features (portfolio sharing, community insights)
- Integration with brokerage APIs for direct trading
- Advanced ML models (Transformer-based time-series)
- Backtesting engine for strategy validation
- Tax optimization suggestions
- ESG scoring integration
