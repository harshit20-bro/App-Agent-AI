// AppAgentAI - MVP Codebase

// === project root structure === 
// app-agent-ai/ 
// ├── public/ 
// ├── src/ 
// │   ├── assets/ 
// │   ├── components/ 
// │   ├── pages/ 
// │   ├── agents/ 
// │   ├── styles/ 
// │   ├── App.tsx 
// │   ├── main.tsx 
// ├── .env 
// ├── firebaseConfig.ts 
// ├── tailwind.config.js 
// ├── index.html 
// ├── package.json

// === FRONTEND: src/main.tsx ===
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import './styles/global.css';
import { BrowserRouter } from 'react-router-dom';

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);

// === FRONTEND: src/App.tsx ===
import { Routes, Route, Navigate } from 'react-router-dom';
import Login from './pages/Login';
import Dashboard from './pages/Dashboard';
import AgentPanel from './pages/AgentPanel';
import { Toaster } from 'react-hot-toast';

function App() {
  return (
    <>
      <Toaster position="top-right" />
      <Routes>
        <Route path="/login" element={<Login />} />
        <Route path="/dashboard" element={<Dashboard />} />
        <Route path="/agent/:appId" element={<AgentPanel />} />
        <Route path="*" element={<Navigate to="/login" />} />
      </Routes>
    </>
  );
}

export default App;

// === BACKEND: firebaseConfig.ts ===
import { initializeApp } from 'firebase/app';
import { getAuth } from 'firebase/auth';
import { getFirestore } from 'firebase/firestore';

const firebaseConfig = {
  apiKey: import.meta.env.VITE_FIREBASE_API_KEY,
  authDomain: import.meta.env.VITE_FIREBASE_AUTH_DOMAIN,
  projectId: import.meta.env.VITE_FIREBASE_PROJECT_ID,
  storageBucket: import.meta.env.VITE_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: import.meta.env.VITE_FIREBASE_MESSAGING_SENDER_ID,
  appId: import.meta.env.VITE_FIREBASE_APP_ID,
};

const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);
export const db = getFirestore(app);

// === PAGES === 
// Login.tsx: handles Google + email/password login 
// Dashboard.tsx: shows list of connected apps + create new agent 
// AgentPanel.tsx: interactive interface for the AI agent (chat + buttons)

// === AGENT SYSTEM === 
// src/agents/AgentManager.ts - manages isolated agents per app 
// src/agents/whatsappAgent.ts - handles WhatsApp logic 
// src/agents/instagramAgent.ts - handles Instagram logic

// === STYLING === 
// Tailwind CSS + custom neon styles in global.css

// === TO INSTALL === 
// npm install react-router-dom firebase react-hot-toast 
// npm install -D tailwindcss postcss autoprefixer 
// npx tailwindcss init -p

// === ENV FILE === 
// .env 
// VITE_FIREBASE_API_KEY=your_api_key 
// VITE_FIREBASE_AUTH_DOMAIN=your_auth_domain 
// VITE_FIREBASE_PROJECT_ID=your_project_id 
// VITE_FIREBASE_STORAGE_BUCKET=your_storage_bucket 
// VITE_FIREBASE_MESSAGING_SENDER_ID=your_msg_id 
// VITE_FIREBASE_APP_ID=your_app_id

// === RUN === 
// npm run dev
