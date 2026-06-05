# EcoSort AI - Smart Plastic Sustainability Platform

EcoSort AI is a complete, full-stack, circular economy web application developed for environmental project competitions. It leverages a Deep Learning Convolutional Neural Network (CNN) model built in TensorFlow to classify plastic types from codes 1-7 (PET, HDPE, PVC, LDPE, PP, PS, and Other) from uploaded photos or live webcam captures.

---

## 🚀 Key Features

1. **Home Page**: Includes a dynamic environmental theme, stats cards, real-time global plastic waste counter, and a recycling facts carousel.
2. **Plastic Scanner (Core)**: Allows webcam capturing and drag-and-drop file uploading. Returns chemical classification, hazard levels, carbon footprints, decomposition times, health/ecological warnings, and alternative material suggestions. Integrates interactive Recharts visualization widgets.
3. **Environmental Impact**: Highlights damage done to oceans, soil, rivers, wildlife, and human health (microplastics, cancer hazards). Features embedded educational documentaries.
4. **Government Initiatives**: Showcases major Indian clean initiatives (Plastic Waste Management Rules, Swachh Bharat SBM, Single-Use Plastic Ban, and EPR portal) alongside impact statistics and policy timelines.
5. **Reward System**: Gamified "EcoCoin" wallet. Log plastic weight (e.g. 1kg to 300kg) to earn EcoCoins, progress towards ranks (Zero-Waste Legend), view community leaderboards, and use a simulated cash-redemption terminal.
6. **About Team**: Credits team members (Rupa Kundu, Debanjana Sarkar, Soumita Das) and supervisor Ms. Arpita Roy.
7. **Thank You Page**: Celebrate milestones with a circular economy exit screen and confetti animations.

---

## 📁 Project Folder Structure

```
plastic/
│
├── backend/
│   ├── app.py                # Main Flask API endpoints
│   ├── plastic_data.py       # Ecological database for resin details
│   ├── report_generator.py   # PDF compiler using fpdf and matplotlib
│   ├── database.db           # SQLite database (auto-generated)
│   ├── requirements.txt      # Python backend dependencies
│   └── temp_uploads/         # Uploaded images directory (auto-generated)
│
├── frontend/
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Home.jsx      # Home dashboard & carousel
│   │   │   ├── Scanner.jsx   # Webcam/upload module & Recharts
│   │   │   ├── Impact.jsx    # Environmental impact & videos
│   │   │   ├── Initiatives.jsx # India clean policy tabs & timeline
│   │   │   ├── Rewards.jsx   # Wallet, leaderboard & coin rain
│   │   │   ├── Team.jsx      # Credits and mentor details
│   │   │   └── ThankYou.jsx  # Final splash & confetti
│   │   ├── App.jsx           # Main tabs routing & theme state
│   │   ├── index.css         # Glassmorphic stylesheet
│   │   └── main.jsx          # React app entrypoint
│   ├── index.html            # Main HTML document
│   └── package.json          # React packages (Recharts, Lucide, Framer)
│
├── plastic_classifier.h5     # Trained TensorFlow CNN Model
└── README.md                 # Complete documentation
```

---

## 🗄️ Database Schema

The backend uses a localized, lightweight **SQLite** database (`backend/database.db`) configured with the following tables:

### 1. `scans` Table
Tracks all scanned items for analytics.
| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | INTEGER (PK, Autoincrement) | Unique Scan ID |
| `plastic_type` | TEXT | E.g. "PET", "HDPE", etc. |
| `confidence` | REAL | CNN model percentage confidence |
| `env_score` | INTEGER | Environmental Risk (0 - 100) |
| `image_name` | TEXT | Path to the saved upload image |
| `timestamp` | DATETIME | Time of prediction (Default: CURRENT_TIMESTAMP) |

### 2. `user_wallet` Table
Maintains the logged-in user profile's total metrics (for demo purposes).
| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | INTEGER (PK) | Single profile ID (value = 1) |
| `total_weight` | REAL | Total weight recycled in kilograms |
| `total_coins` | INTEGER | Total earned EcoCoins |

### 3. `leaderboard` Table
Maintains competitive scores for community members.
| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | INTEGER (PK, Autoincrement) | Entry ID |
| `name` | TEXT | Member's display name |
| `coins` | INTEGER | Total coins score |

---

## 💻 Local Setup & Deployment

### 1. Run the Backend API
Navigate to the `backend` folder, install requirements, and boot up the Flask server:
```powershell
# Navigate into backend
cd backend

# Install dependencies
py -3.11 -m pip install -r requirements.txt

# Start Flask API
py -3.11 app.py
```
*The Flask server will start running on **`http://localhost:5000`**.*

### 2. Run the React Frontend
Open a **new terminal tab**, navigate to the `frontend` folder, install node packages, and launch Vite's dev server:
```powershell
# Navigate into frontend
cd frontend

# Install node dependencies
npm install

# Start Vite server
npm run dev
```
*Vite will compile and launch the app. Open **`http://localhost:5173`** in your web browser.*

### 3. Run the Streamlit Frontend (Python Alternative)
Open a **new terminal tab**, navigate to the `frontend2` folder, install python requirements, and launch Streamlit:
```powershell
# Navigate into frontend2
cd frontend2

# Install dependencies
py -3.11 -m pip install -r requirements.txt

# Start Streamlit server
py -3.11 -m streamlit run app.py
```
*Streamlit will compile and launch the app. Open **`http://localhost:8501`** in your web browser.*

---

## 🛡️ Model Inference Fallback Mode
If your computer fails to load the heavy 134MB `plastic_classifier.h5` file (due to hardware limitations or driver mismatches), the backend Flask server automatically switches to an **Inference Fallback Simulation Mode**. This mimics model inference with realistic predictions and allows full testing of the charts, wallet transactions, and PDF reports without any crashes.
