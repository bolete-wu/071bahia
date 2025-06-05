/bet-app
  /backend
    - server.js
    - routes.js
    - controllers.js
    - models.js
  /frontend
    /src
      - App.jsx
      - components/
      - pages/
      - styles/
  - package.json
  - README.npx create-react-app frontend
cd frontend
npm install -D tailwindcss
npx tailwindcss module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
import React from 'react';
import './styles/tailwind.css';

function App() {
  return (
    <div className="bg-gray-900 text-white min-h-screen flex items-center justify-center">
      <div className="text-center">
        <h1 className="text-4xl font-bold mb-4">Bem-vindo à BetBlaze</h1>
        <button className="bg-red-600 hover:bg-red-700 px-6 py-3 rounded-lg">
          Apostar Agora
        </button>
      </div>
    </div>
  );
}

export default mkdir backend
cd backend
npm init -y
npm install express pg bcryptjs jsonwebtoken cors const express = require('express');
const cors = require('cors');
const routes = require('./routes');
require('dotenv').config();

const app = express();

app.use(cors());
app.use(express.json());

app.use('/api', routes);

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => console.log(`Server running on port ${const express = require('express');
const router = express.Router();
const { registerUser, loginUser, placeBet, getGames } = require('./controllers');

// Rotas de autenticação
router.post('/register', registerUser);
router.post('/login', loginUser);

// Rotas de apostas
router.post('/bet', placeBet);
router.get('/games', getGames);

module.exports = const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');

const users = [];  // Apenas para teste. Ideal: usar banco de dados.

exports.registerUser = async (req, res) => {
  const { username, password } = req.body;
  const hashed = await bcrypt.hash(password, 10);
  users.push({ username, password: hashed });
  res.json({ message: 'Usuário registrado' });
};

exports.loginUser = async (req, res) => {
  const { username, password } = req.body;
  const user = users.find(u => u.username === username);
  if (user && await bcrypt.compare(password, user.password)) {
    const token = jwt.sign({ username }, 'secretkey', { expiresIn: '1h' });
    res.json({ token });
  } else {
    res.status(401).json({ message: 'Credenciais inválidas' });
  }
};

exports.placeBet = (req, res) => {
  const { game, amount } = req.body;
  // lógica simplificada
  const win = Math.random() < 0.5;
  res.json({ game, amount, result: win ? 'Win' : 'Lose' });
};

exports.getGames = (req, res) => {
  res.json([{ id: 1, name: 'Crash' }, { id: 2, name: 'Double' }]);
const { Pool } = require('pg');
const pool = new Pool({
  connectionString: process.env.DATABASE_URL,
});

module.exports = // Exemplo fictício
exports.processPayment = (req, res) => {
  const { amount } = req.body;
  // Chamar API de pagamento
  res.json({ status: 'Pagamento processado', amount });
exports.playCrash = (req, res) => {
  const multiplier = (Math.random() * 10).toFixed(2);
  res.json({ multiplier });
};
