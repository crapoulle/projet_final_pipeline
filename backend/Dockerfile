# --- Étape 1 : Build / installation des dépendances ---
FROM node:18-alpine AS builder

WORKDIR /app

# Copier uniquement les fichiers NPM pour installer les dépendances plus vite
COPY package*.json ./
RUN npm install --production

# Copier le reste du code
COPY . .

# --- Étape 2 : Image finale, plus légère ---
FROM node:18-alpine

WORKDIR /app

# Copier les fichiers depuis l'étape builder
COPY --from=builder /app /app

# Variables d'environnement (peuvent être remplacées au runtime)
ENV NODE_ENV=production
# ⚠️ NE PAS mettre tes vraies clés ici
# Elles seront injectées plus tard via docker run ou docker-compose

EXPOSE 5001

CMD ["node", "server.js"]
