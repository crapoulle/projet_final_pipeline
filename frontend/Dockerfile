# ---- Étape 1 : Build du frontend ----
FROM node:20-alpine AS builder

WORKDIR /app

# Copier uniquement package.json + lock pour optimiser le cache
COPY package*.json ./

# Installer les dépendances
RUN npm install --legacy-peer-deps

# Copier le reste du code source
COPY . .

# Build en production
RUN npm run build

# ---- Étape 2 : Image finale, légère pour servir le build ----
FROM node:20-alpine

WORKDIR /app

# Installer serve uniquement dans l'image finale
RUN npm install -g serve

# Copier le build compilé
COPY --from=builder /app/build ./build

# Variable ENV (⚠ doit être injectée depuis docker-compose ou runtime)
ENV REACT_APP_API_KEY=""

EXPOSE 3000

# Lancer l'app
CMD ["serve", "-s", "build", "-l", "3000"]

