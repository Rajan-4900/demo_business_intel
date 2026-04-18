# 📍 Crowd Heatmap & Business Intelligence Platform

[![Python Version](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)
[![Django Version](https://img.shields.io/badge/django-6.0-green.svg)](https://www.djangoproject.com/)
[![AI](https://img.shields.io/badge/AI-Google%20Gemini-orange.svg)](https://ai.google.dev/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

An advanced Business Intelligence (BI) tool designed to help entrepreneurs and businesses identify high-potential locations using real-time crowd density analysis and machine learning insights.

---

## 🚀 Key Features

### 📊 Real-Time Crowd Heatmap
Analyze foot traffic and POI (Point of Interest) density within a **5km radius** of any location in India. Using the OpenStreetMap (OSM) Overpass API, the platform partitions areas into high, medium, and low-intensity sectors.

### 🤖 AI-Powered Business Recommendations
Leverages a **Scikit-Learn** predictive model and **Google Gemini 1.5 Pro** to suggest the most viable business types for a specific area. It considers crowd intensity, area type (Commercial, Residential, Industrial), and local competition.

### 💰 Revenue & Feasibility Engine
- **Smart Revenue Forecast**: Estimates potential monthly revenue using local market data and crowd scores.
- **Feasibility Checker**: Validates your business idea against the current local landscape to provide a "Go/No-Go" recommendation.

### 💬 Intelligent Support Bot
A built-in AI assistant powered by Google Gemini that provides real-time guidance on navigating the platform and strategic business advice based on live data.

---

## 💰 Deep Dive: Revenue AI Logic

The platform employs a multi-factor simulation engine to estimate financial viability:

- **Footfall Simulation**: Calculated using local POI density filtered through **Temporal Multipliers**. Traffic varies dynamically based on time-of-day (e.g., 1.6x multiplier for Evening Peaks vs 0.2x for Late Night).
- **Customer Quality Index (CQI)**: A weighted spending power metric derived from the neighborhood mix.
    - *Professionals*: 1.8x spending weight.
    - *Students*: 0.6x spending weight.
    - *Tourists/Families*: 2.5x / 1.3x weights respectively.
- **Conversion & Overload Modifiers**: 
    - **Competition Density**: Reduces conversion rate if similar POIs are saturated.
    - **Service Fatigue (Overload Penalty)**: Revenue is penalized if forecasted footfall exceeds the business's **Optimal Capacity Range**, simulating wait-time friction and lost customers.

## ✅ Feasibility Analysis Engine

The feasibility engine provides a **Go/No-Go** recommendation by cross-referencing three data layers:

1.  **Intensity Mapping**: Checks if the business type (e.g., Pharmacy vs. Cafe) historically thrives in the detected crowd intensity (High/Medium/Low).
2.  **Dynamic Local Proof**: Scans for "Live Evidence" by detecting existing successful businesses of the same category in the immediate sector.
3.  **ML Inference**: Uses the Scikit-Learn model to predict the "Best Fit" business for the specific area type (Commercial, Residential, etc.).

## 📍 Smart Relocation (AI Zones)

When a location is analyzed, the AI generates **High-Potential AI Zones** within a ~1.7km radius:

- **Candidate Scanning**: Evaluates multiple spatial offsets to identify "hotter" zones that the user might have missed.
- **Composite Scoring**: Locations are ranked 0-100 based on:
    - **Footfall Potential** (30%)
    - **Demand-Supply Gap** (15%)
    - **Area Growth Potential** (15%)
    - **Spending Power & Competition Density** (40%)

---

## 🛠️ Technology Stack

- **Backend**: Django 6.0, Django Channels (WebSockets)
- **Frontend**: Responsive HTML5, Vanilla CSS3, Javascript (ES6+)
- **Machine Learning**: Scikit-Learn, Pandas, NumPy
- **Generative AI**: Google Generative AI (Gemini 1.5 Pro)
- **Data Sources**: OpenStreetMap (Nominatim & Overpass API)
- **Database**: SQLite (Development) / PostgreSQL (Production ready)
- **Asynchronous Server**: Daphne / ASGI

---

## ⚙️ Getting Started

### Prerequisites
- Python 3.10 or higher
- A Google AI Studio API Key (for Gemini Chatbot/Analysis)

### 1. Clone & Navigate
```powershell
git clone <your-repo-url>
cd "final_crowd_heatmap-main/crowd_heatmap_final"
```

### 2. Environment Setup
Create a `.env` file in the `crowd_heatmap_final` directory:
```env
GEMINI_API_KEY=your_google_api_key_here
SECRET_KEY=your_django_secret_key
DEBUG=True
```

### 3. Installation
It is highly recommended to use a virtual environment:
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1  # Windows
pip install -r requirements.txt
```

### 4. Database Migrations
```powershell
python manage.py makemigrations
python manage.py migrate
```

### 5. Running the Application
For regular development:
```powershell
python manage.py runserver
```
For WebSocket support (Chatbot):
```powershell
daphne -p 8000 crowd_heatmap_project.asgi:application
```

Access the platform at `http://127.0.0.1:8000`.

---

## 📁 Project Structure

```text
crowd_heatmap_final/
├── crowd_heatmap_project/   # Core Configuration (settings, asgi, wsgi)
├── heatmap_app/             # Main Logic (Views, ML models, Heatmap utils)
├── users/                   # Custom User Management & Authentication
├── templates/               # UI Templates (Home, Dashboard, Recommendations)
├── static/                  # Assets (CSS, JS, Images)
├── requirements.txt         # Project Dependencies
└── manage.py                # Django CLI
```

---

## 📖 User Guide

1.  **Search**: Enter a location in India to center the map.
2.  **Detection**: Click "Find My Location" to use browser-based geolocation.
3.  **Analyze**: Use "Find Popular Places (5km)" to trigger the crowd density engine.
4.  **Forecast**: Open the Dashboard to view revenue predictions and feasibility scores.
5.  **AI Insights**: Ask the chatbot for specific business advice for the currently selected area.

---

## 🗺️ Documentation Links

- [Detailed Run Instructions](crowd_heatmap_final/RUN_INSTRUCTIONS.md)
- [Geolocation & Map Guide](crowd_heatmap_final/GEOLOCATION_GUIDE.md)
- [Auth Structure Summary](crowd_heatmap_final/AUTH_STRUCTURE_SUMMARY.md)

---

## 📄 License
Distributed under the MIT License. See `LICENSE` for more information.
