# Roamio Agent Context

## 🎯 Core Purpose

Roamio is a full-stack location-based quest generator that transforms everyday exploration into immersive real-world adventures.

---

## 🛠️ Tech Stack Overview

- **Frontend:** React.js + Tailwind CSS (hosted on Firebase Hosting or Google Cloud Run)
- **Backend:** FastAPI (Python, on Google Cloud Run)
- **Database:** Google Firestore
- **Auth:** Firebase Authentication (Google OAuth2)
- **APIs:**
  - Google Maps + Directions API (routing and ETA)
  - Google Places API (landmark data)
  - OpenAI API (quest and postcard generation)

---

## 🧠 Product Features

### ✅ Minimum Demo Scope
- **Quest Generation:**
  - Enter a location or use GPS
  - Select quest mood/style
  - Generate quest via OpenAI with 3–5 location stops
- **QuestLivePage:**
  - Starts with user's GPS location
  - Map shows route and progress
  - ETA + stop completion tracking
- **QuestDetails:**
  - Save completed quest to Firestore
  - Generate stylized image (postcard)
- **Profile Page:**
  - Show completed quests, badges, difficulty stats

---

## 🗺️ Quest Flow

1. User generates a quest from `QuestHome`
2. User starts quest → navigates to `QuestLivePage`
3. Route includes:
   - Current GPS → 3–5 Places
   - Google Directions API used for path
4. User marks stops as visited
5. Upon completion:
   - Quest is saved to Firestore
   - Stylized image generated using OpenAI
   - Postcard shown in profile

---

## 📦 Firestore Structure

/users/{userId}
→ { displayName, email, lastActive }

/quests/{locationHash_mood}
→ { questText, locationList, timestamp, usageCount }

/user_quests/{userId}/{questId}
→ { questIdRef, generatedAt, completedAt, imageUrl, difficulty }

yaml
Copy
Edit

---

## 🔐 Security

- All API keys are stored in Google Secret Manager
- Firebase Auth is required for generating or saving quests
- Rate limit: 3 quests per user per day (enforced server-side)

---

## 🔄 Development Philosophy

- **Live-first UI testing**
- **Small, validated PR-style changes**
- **Readable diffs and patch notes**
- **Every task must push forward end-user journey**

---

## 🤖 Agent Rulebook

- Start every task by checking if necessary files/components exist
- Validate by launching app on `localhost:5173`
- Use browser GPS API for live location
- When unclear, halt and ask for clarification
- Save changes cleanly and explain each one
- Push validated changes before beginning next task
