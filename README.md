 
> A data-driven, cloud-hosted web application that ranks NBA players objectively using advanced statistical modelling — eliminating media bias and subjectivity from player evaluation.
 
![Tech Stack](https://img.shields.io/badge/Frontend-React_18_+_Vite-61DAFB?style=flat-square&logo=react)
![Backend](https://img.shields.io/badge/Backend-R_+_Plumber-276DC3?style=flat-square&logo=r)
![Hosting](https://img.shields.io/badge/Hosting-Firebase_+_GCP-FFCA28?style=flat-square&logo=firebase)

 
---
 
## 📖 Overview
 
Traditional NBA rankings from ESPN, The Ringer, and media outlets are heavily influenced by popularity, narratives, and subjective opinions rather than on-court performance. This project addresses that gap.
 
The **NBA Player Ranking Website** evaluates players purely on measurable performance metrics, grouped into 6 statistical categories and scored on a familiar **30–99 scale** (like trading cards). The platform delivers three core analytical features:
 
| Feature | Description |
|---|---|
| 🏆 **Rankings Dashboard** | Real-time player rankings updated weekly via automated pipeline |
| ⚡ **Hot & Cold Streaks** | Rolling 5-game and 10-game form trends across the NBA |
| ⚖️ **Player Comparison Tool** | Side-by-side comparison of up to 4 players with radar chart visualisation |
 
---
 
## 📸 Screenshots
 
### Player Rankings
<img width="583" height="698" alt="Screenshot 2026-03-23 at 1 34 55 AM" src="https://github.com/user-attachments/assets/fe0137ab-bd97-44a5-bc63-9f420d326a5d" />

 
### Player Comparison
 <img width="581" height="684" alt="Screenshot 2026-03-23 at 1 35 32 AM" src="https://github.com/user-attachments/assets/4019e915-62fc-4a28-97d1-313a94d95e44" />

### Hot & Cold Streaks
<img width="584" height="291" alt="Screenshot 2026-03-23 at 1 36 17 AM" src="https://github.com/user-attachments/assets/1eeb79bd-be1b-4750-a066-32ce9d5107de" />

 
---
 
## 🧠 Statistical Model
 
Players are ranked using **18 statistics** grouped into 6 weighted categories:
 
| Category | Focus |
|---|---|
| **Impact** | Overall game influence, plus/minus |
| **Scoring** | Points, efficiency, shot selection |
| **Playmaking** | Assists, turnovers, creation |
| **Rebounding** | Offensive and defensive boards |
| **Discipline** | Fouls, turnovers, consistency |
| **Defense** | Steals, blocks, defensive rating |
 
**How it works:**
- Each stat is standardised using **z-score normalisation**
- Category scores are blended using fixed weights into an overall score
- Scores are mapped to a **30–99 scale** using a logistic function for easy interpretation
- Short-term form uses **rolling 5-game and 10-game averages** with minimum minute thresholds to ensure only active players are ranked
 
---
 
## 🏗️ Architecture
 
```
┌─────────────────────────────────────────────────┐
│                    BACKEND                       │
│  hoopR / NBAstatR → R Script → Cloud Scheduler  │
│              → CSV files in Cloud Storage        │
└──────────────────────┬──────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────┐
│                  INTEGRATION                     │
│         R Plumber API → Google Cloud Run         │
│    Endpoints: /rankings  /compare  /trends       │
└──────────────────────┬──────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────┐
│                  FRONTEND                        │
│     React 18 + Vite 5 + Tailwind CSS v3         │
│          Axios + Recharts → Firebase             │
└─────────────────────────────────────────────────┘
```
 
---
 
## 🛠️ Tech Stack
 
### Frontend
- **React 18** with Vite 5 for fast builds and hot reloading
- **Tailwind CSS v3** for utility-first responsive styling
- **Recharts** for interactive radar chart on the comparison page
- **Axios** for API data fetching
- **Firebase Hosting** for deployment and scalability
 
### Backend & Data
- **R** with `hoopR` and `nbastatR` packages for NBA data ingestion
- **R Plumber** for REST API layer exposing 3 read-only endpoints
- **Google Cloud Run** for containerised, serverless API hosting
- **Google Cloud Storage** for precomputed CSV datasets
- **Google Cloud Scheduler** for automated weekly data refresh
 
### Testing
- **Selenium** for automated UI smoke testing and concurrent load simulation
- Validated system stability under **100 simultaneous browser instances** across multiple browsers and network conditions
 
---
 
## 🌐 Deployment
 
The application was deployed and hosted on **Firebase** with a cloud-hosted R Plumber API running on **Google Cloud Run**, automatically refreshed weekly via **Google Cloud Scheduler**.
https://nba-ranking-ds-01.web.app/ — ⚠️ Data pipeline currently offline

 
---
 
## ✅ Requirements Traceability
 
All 9 requirements delivered at **100% completion:**
 
| ID | Requirement | Type | Status |
|---|---|---|---|
| R01 | Real-time interactive player ranking dashboard | Functional | ✅ 100% |
| R02 | Compare up to 4 players by grouped stats | Functional | ✅ 100% |
| R03 | Visualise hot/cold player streaks over selected games | Functional | ✅ 100% |
| R04 | Auto-refresh player data weekly via open NBA API | Functional | ✅ 100% |
| R05 | Filter rankings by team, conference, position and search | Functional | ✅ 100% |
| R06 | Dashboard loads within 10 seconds under standard conditions | Performance | ✅ 100% |
| R07 | Accessible on all modern browsers on a standard PC display | UI | ✅ 100% |
| R08 | Intuitive for casual NBA fans with no training required | Usability | ✅ 100% |
| R09 | Scalable to handle 100+ simultaneous users | Performance | ✅ 100% |
 
---
 
## 👥 Team — DS_01
 
| Name | Role | Responsibilities |
|---|---|---|
| **Krispin Martin** | Project Manager | Frontend/Backend Support, Cloud Hosting, Agile Practices |
| **Aldrich Liem** | Data Engineer | Backend Development, Ranking Algorithm, Cloud Scheduler |
| **Samiul Hoque** | QA Lead | Risk Management, Selenium Testing, Frontend Support |
| **Shlok Trivedi** | Software Developer | UI Implementation, Visualisations, Page Setup |
 
---
 
## 🔮 Future Improvements
 
- **Historical season data** — compare player performance across multiple seasons for longitudinal analysis
- **Additional visualisations** — dynamic rank progression charts on the Trends page
- **Predictive analytics** — match outcome projections and fantasy-focused tools
- **Expanded audience** — sports betting analytics targeting the growing Australian and US markets
 
---
 
## 📚 References
 
- Singh et al. (2022). *Evaluating basketball player performance: A review of traditional and advanced statistical models.* Journal of Sports Analytics, 8(2), 105–123.
- Alagappan et al. (2020). *Data-driven basketball analytics: Bridging the gap between insight and accessibility.* MIT Sloan Sports Analytics Conference.
- Soebbing & Humphreys (2020). *Media market size and biases in award voting.* Journal of Sports Economics, 21(1), 3–25.
 
---
 
*Developed as part of **FIT3164 Data Science Project** — Monash University, 2025*
 
