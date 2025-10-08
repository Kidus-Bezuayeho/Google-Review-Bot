# Google Review Bot Implementation Plan

## Overview

Build a complete Google Review Bot with Google My Business API integration, Gemini AI auto-replies, Gmail notifications, and SQLite state management.

### Dependencies & Configuration

- **Update `requirements.txt`** with:
- `google-auth`, `google-auth-oauthlib`, `google-auth-httplib2` (Google OAuth)
- `google-api-python-client` (GMB & Gmail APIs)
- `google-generativeai` (Gemini AI)
- `python-dotenv` (environment variables)
- **Create `.env.example`** template for required credentials
- **Create `config.py`** to load environment variables


## Implementation Steps

### 1. Database Setup

- **Create `database/` folder** with:
- `schema.sql` - SQLite schema for tracking processed reviews
- `db_manager.py` - Database initialization and query functions
- Track: review_id, rating, processed_at, action_taken (replied/emailed)

### 2. Google API Authentication

- **Create `auth/` folder** with:
- `google_auth.py` - OAuth flow for GMB & Gmail APIs
- Setup functions to generate and refresh tokens
- Store credentials in `credentials.json` and `token.json`

### 3. Service Implementations

#### `services/fetch_reviews.py`

- Authenticate with Google My Business API
- Fetch recent reviews from business location
- Return list of review objects with: id, rating, text, author, timestamp

#### `services/classify_reviews.py`

- Simple rating classifier:
- Ratings 1-3: "negative" 
- Ratings 4-5: "positive"
- Check SQLite to filter out already-processed reviews

#### `services/generate_reply.py`

- Initialize Gemini AI client
- Create prompt template for professional responses
- Generate personalized reply based on review text
- Post reply back to Google My Business API

#### `services/send_email.py`

- Authenticate with Gmail API
- Compose alert email with review details
- Send to configured recipient email
- Include review text, rating, author, link to review

### 4. Main Orchestration

- **Update `main.py`**:
- Initialize database
- Fetch new reviews
- Classify each review
- For positive (4-5 stars): generate and post AI reply
- For negative (1-3 stars): send email alert
- Update SQLite with processed reviews
- Error handling and logging

### 5. Scheduling Setup

- **Create `scheduler.py`** or cron instructions:
- Schedule main.py to run daily at 12:00 PM
- Include both local cron and Cloud Scheduler examples

### 6. Documentation

- **Update README.md** with:
- Setup instructions (API credentials, OAuth flow)
- Environment variables required
- How to run locally and deploy to cloud
- Troubleshooting section

## Key Files to Create/Modify

- `requirements.txt` - Add all dependencies
- `config.py` - Environment configuration
- `database/schema.sql` - SQLite schema
- `database/db_manager.py` - Database operations
- `auth/google_auth.py` - OAuth authentication
- `services/fetch_reviews.py` - GMB API integration
- `services/classify_reviews.py` - Review classification
- `services/generate_reply.py` - Gemini AI + reply posting
- `services/send_email.py` - Gmail API integration
- `main.py` - Main orchestration logic
- `.env.example` - Environment template
- `README.md` - Complete setup guide