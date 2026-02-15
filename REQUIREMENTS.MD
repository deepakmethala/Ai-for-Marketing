# Requirements Document

## Project Overview

**Project Name:** SECTORWISE AI – Intelligent Sector-Based Investment Allocation Engine

**Team:** COODY BLINDERS

**Team Lead:** PHANINDER REDDY

**Target Users:** Beginner retail investors

**Platform:** Web Application

**Language:** English

**Core Objective:** Create a beginner-friendly AI-driven investment platform that analyzes stocks within selected sectors, scores them using a multi-factor weighted AI model, allocates capital optimally, and simulates future scenarios with risk-adjusted allocation dashboards.

## Functional Requirements

### Core Features

#### 1. User Input Collection
- Accept investment amount from user
- Allow sector selection from 7 sectors: IT, Banking & Finance, Pharmaceutical, Automobile, FMCG, Defence, Power
- Capture risk profile: Low / Medium / High
- Capture time horizon: 1Y / 3Y / 5Y / 10Y

#### 2. Stock Analysis Engine
- Calculate fundamental metrics: P/E Ratio, PEG Ratio, P/B Ratio, ROE, ROCE, Debt-to-Equity, 5-Year Revenue CAGR, 5-Year Profit CAGR, Promoter Holding %, Promoter Pledge %, Free Cash Flow trend, Interest Coverage Ratio
- Calculate technical indicators: RSI (14), MACD, 50 DMA, 200 DMA, Volatility (Std Dev), Beta
- Calculate sentiment metrics: News Sentiment Score, Institutional Flow Score, Social Sentiment Index

#### 3. Scoring Model
- Implement weighted scoring engine with:
  - 40% Fundamental Score
  - 30% Technical Score
  - 20% Sector Momentum Score
  - 10% Sentiment Score
- Normalize all values between 0-100

#### 4. Capital Allocation Engine
- Allocate capital based on stock scores
- Apply risk-based adjustments
- Enforce diversification rules:
  - Max 40% in one stock
  - Minimum 3 stocks per allocation
  - Volatility cap based on risk profile

#### 5. Prediction Engine
- Implement 3 ML models: Random Forest Regressor, XGBoost, LSTM
- Generate expected return ranges (1Y) with Best Case, Worst Case, and Probability distribution
- Never show guaranteed returns

#### 6. Scenario Simulation
- Display Conservative (25th percentile), Expected (50th percentile), and Aggressive (75th percentile) scenarios
- Calculate Sharpe Ratio, Max Drawdown, Portfolio Volatility

#### 7. Marriage Proposal Score
- Create compatibility score out of 100 evaluating: Earnings consistency, Debt health, Valuation fairness, Promoter trust, Growth potential
- Display as circular UI meter

### User Stories

- As a beginner investor, I want to input my investment amount and risk profile so that I receive personalized stock recommendations
- As a user, I want to select specific sectors so that my portfolio aligns with my investment preferences
- As a user, I want to see AI-driven stock scores so that I understand which stocks are recommended and why
- As a user, I want to view scenario simulations so that I can understand potential outcomes
- As a user, I want to see risk metrics so that I can make informed decisions
- As a user, I want explainable AI insights so that I understand the reasoning behind allocations

## Non-Functional Requirements

### Performance

- API response time < 2 seconds for stock analysis
- ML model prediction time < 5 seconds
- Dashboard load time < 3 seconds
- Support concurrent users with auto-scaling

### Security

- JWT Authentication for user sessions
- Encrypted database connections
- Rate limiting on API endpoints
- Input validation on all user inputs
- Secure storage of user data
- AWS Cognito for authentication management

### Scalability

- Horizontal scaling via AWS Lambda
- Database optimization for large datasets
- Caching strategy for frequently accessed data
- CDN for static assets

### Usability

- Beginner-friendly interface with tooltips
- Responsive design for mobile and desktop
- Dark and light mode support
- Clean fintech theme with glassmorphism cards
- Animated charts for better visualization

### Compliance

- Display ethical disclaimer: "This platform provides AI-driven probabilistic analysis for educational purposes only and does not guarantee returns or constitute financial advice."
- No guaranteed return claims
- Transparency in scoring methodology

## Constraints

- Must use AWS infrastructure (Amplify, Lambda, API Gateway, EC2, RDS, S3, SageMaker, Comprehend, Forecast, Cognito, CloudWatch)
- Must support 7 specific sectors only
- Must maintain explainability in AI decisions
- Must prioritize risk control
- Code must be modular, clean, and production-structured

## Success Criteria

- Successfully analyze and score stocks across all 7 sectors
- Provide accurate capital allocation based on user risk profile
- Generate scenario simulations with probability distributions
- Achieve < 3 second dashboard load time
- Pass security audit for authentication and data protection
- Receive positive feedback from beginner investors on usability
- Successfully deploy on AWS with monitoring enabled
- Demonstrate AI explainability in allocation decisions
