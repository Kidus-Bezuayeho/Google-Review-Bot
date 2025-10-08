# Google Review Bot Implementation Plan

## 🎯 Project Overview
Build an automated Google Review Bot that:
- Fetches reviews from Google My Business API
- Classifies reviews by rating (1-3 stars = negative, 4-5 stars = positive)
- Auto-replies to positive reviews using Gemini AI
- Sends Gmail alerts for negative reviews
- Runs daily at 12:00 PM to check for new reviews

## 🏗️ Architecture Decisions
- **Google API**: Google My Business API for fetching reviews
- **Email Service**: Gmail API for sending alerts
- **AI Service**: Gemini AI for generating responses
- **Database**: SQLite for tracking processed reviews
- **Authentication**: OAuth2 for Google APIs
- **Scheduling**: Daily at 12:00 PM

## 📋 Implementation Steps

### Phase 1: Foundation Setup ✅
- [x] Create virtual environment (`ReviewBot`)
- [x] Set up dependencies in `requirements.txt`
- [x] Configure `.gitignore` for virtual environment
- [ ] Create `.env.example` template
- [ ] Create `config.py` for environment variables

### Phase 2: Database Layer
- [ ] Create `database/` folder
- [ ] Design SQLite schema (`schema.sql`)
- [ ] Implement database manager (`db_manager.py`)
- [ ] Track: review_id, rating, processed_at, action_taken

### Phase 3: Authentication
- [ ] Create `auth/` folder
- [ ] Implement Google OAuth flow (`google_auth.py`)
- [ ] Handle token refresh and storage
- [ ] Support both GMB and Gmail API authentication

### Phase 4: Core Services

#### 4.1 Fetch Reviews (`services/fetch_reviews.py`)
- [ ] Authenticate with Google My Business API
- [ ] Fetch recent reviews from business location
- [ ] Return structured review data:
  - `id`: Review identifier
  - `rating`: Star rating (1-5)
  - `text`: Review content
  - `author`: Reviewer name
  - `timestamp`: Review date

#### 4.2 Classify Reviews (`services/classify_reviews.py`)
- [ ] Simple rating-based classification:
  - 1-3 stars → "negative"
  - 4-5 stars → "positive"
- [ ] Check SQLite for already-processed reviews
- [ ] Return only new, unprocessed reviews

#### 4.3 Generate Replies (`services/generate_reply.py`)
- [ ] Initialize Gemini AI client
- [ ] Create professional response templates
- [ ] Generate personalized replies based on review content
- [ ] Post replies back to Google My Business API

#### 4.4 Send Email Alerts (`services/send_email.py`)
- [ ] Authenticate with Gmail API
- [ ] Compose alert emails with review details
- [ ] Include review text, rating, author, and link
- [ ] Send to configured recipient email

### Phase 5: Main Orchestration
- [ ] Update `main.py` with complete workflow:
  - Initialize database connection
  - Fetch new reviews from GMB
  - Classify each review by rating
  - For positive reviews: generate and post AI reply
  - For negative reviews: send email alert
  - Update database with processed reviews
  - Implement error handling and logging

### Phase 6: Scheduling & Deployment
- [ ] Create scheduling configuration
- [ ] Document local cron setup
- [ ] Provide Cloud Scheduler examples
- [ ] Test daily execution

### Phase 7: Documentation & Testing
- [ ] Update README with complete setup guide
- [ ] Document API credential setup process
- [ ] Add troubleshooting section
- [ ] Create test scenarios

## 🔧 Required Environment Variables

```bash
# Google API Credentials
GOOGLE_CREDENTIALS_FILE=credentials.json
GEMINI_API_KEY=your_gemini_api_key_here

# Business Information
BUSINESS_ACCOUNT_ID=your_business_account_id
LOCATION_ID=your_location_id

# Email Configuration
ALERT_EMAIL=your_email@example.com
```

## 📁 Project Structure

```
Google-Review-Bot/
├── main.py                 # Main orchestration
├── config.py              # Environment configuration
├── requirements.txt       # Dependencies
├── .env.example          # Environment template
├── .gitignore           # Git ignore rules
├── README.md            # Project documentation
├── IMPLEMENTATION_PLAN.md # This file
├── auth/
│   └── google_auth.py   # OAuth authentication
├── database/
│   ├── schema.sql       # SQLite schema
│   └── db_manager.py   # Database operations
└── services/
    ├── fetch_reviews.py    # GMB API integration
    ├── classify_reviews.py # Review classification
    ├── generate_reply.py   # Gemini AI + reply posting
    └── send_email.py       # Gmail API integration
```

## 🚀 Getting Started

1. **Set up virtual environment** (already done)
2. **Install dependencies**: `pip install -r requirements.txt`
3. **Create `.env` file** from `.env.example`
4. **Set up Google API credentials**
5. **Initialize database**
6. **Test each service individually**
7. **Run main orchestration**

## 🔑 Key Learning Points

- **OAuth2 Flow**: Understanding Google API authentication
- **API Integration**: Working with Google My Business and Gmail APIs
- **AI Integration**: Using Gemini for natural language generation
- **Database Design**: SQLite schema for state management
- **Error Handling**: Robust error handling for production use
- **Scheduling**: Automated task execution

## 📚 Next Steps

1. Start with Phase 1: Complete foundation setup
2. Move to Phase 2: Database layer
3. Implement authentication (Phase 3)
4. Build services one by one (Phase 4)
5. Integrate everything in main.py (Phase 5)

---

*This plan provides a structured approach to building the Google Review Bot while learning key concepts in API integration, AI, and automation.*
