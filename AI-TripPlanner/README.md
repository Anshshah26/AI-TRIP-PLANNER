AI TRIP PLANNER

==================================================
PROJECT OVERVIEW
================

AI Trip Planner is a full-stack MERN application that generates intelligent and personalized travel itineraries using AI and open-source services.

It integrates:

* Google Gemini AI for smart itinerary generation
* OpenStreetMap for map data
* OSRM for routing and navigation

The project is designed to work entirely on FREE APIs with a scalable and production-ready architecture.

---

## KEY FEATURES

* AI-powered trip itinerary generation
* Personalized planning based on budget, duration, and interests
* Multi-day trip support (1–30+ days)
* Cost breakdown for activities
* Real-time maps and routing
* Nearby place discovery (restaurants, attractions, etc.)
* Secure JWT authentication system
* Responsive modern UI
* Real-time updates using Socket.IO

---

## TECH STACK

Frontend:

* React.js
* Tailwind CSS
* Framer Motion
* React Query
* Axios
* React Leaflet

Backend:

* Node.js
* Express.js
* MongoDB
* Mongoose
* JWT Authentication
* bcrypt
* Socket.IO

External Services (FREE):

* Google Gemini AI
* OpenStreetMap
* Nominatim
* Overpass API
* OSRM

---

## PROJECT STRUCTURE

AI-TripPlanner/
│
├── client/        -> React Frontend
├── server/        -> Node Backend
├── models/        -> Database Schemas
├── routes/        -> API Routes
├── services/      -> External Integrations
└── README.md

---

## INSTALLATION

1. Clone the repository:
   git clone https://github.com/Anshshah26/AI-TRIP-PLANNER/edit/main/AI-TripPlanner

2. Move into project directory:
   cd AI-TripPlanner

3. Install all dependencies:
   npm run install-all

---

## RUN APPLICATION

Start both frontend and backend:
npm run dev

---

## ACCESS URLS

Frontend: http://localhost:3000
Backend : http://localhost:5000

---

## ENVIRONMENT VARIABLES (server/.env)

PORT=5000
MONGODB_URI=your_database_url
JWT_ACCESS_SECRET=your_access_secret
JWT_REFRESH_SECRET=your_refresh_secret
GEMINI_API_KEY=your_api_key

---

## SECURITY FEATURES

* JWT Authentication (Access + Refresh Tokens)
* Password hashing using bcrypt
* Rate limiting on APIs
* CORS protection
* HTTP-only cookies
* Account lockout after failed attempts

---

## LIMITATIONS

* No hotel or flight booking integration
* No offline mode
* Free API rate limits apply
* AI output depends on input quality

---

## FUTURE IMPROVEMENTS

* Collaborative trip planning
* Mobile app (React Native)
* Offline support (PWA)
* Multi-language support
* Advanced cost optimization

---

## DEPLOYMENT

Frontend: Vercel
Backend : Render

---

## LICENSE

MIT License


==================================================
END OF README
=============
