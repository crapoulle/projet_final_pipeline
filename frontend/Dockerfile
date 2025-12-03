FROM node:20

WORKDIR /app

# Copie des fichiers package.json / package-lock.json
COPY package*.json ./

# Installation des dépendances (important pour installer react-scripts)
RUN npm install --legacy-peer-deps

# Copie du projet complet
COPY . .

# Variable d'environnement (à mettre idéalement via .env ou docker run)
ENV REACT_APP_API_KEY=frontend-api-key-123456

# Build du frontend
RUN npm run build

# Installe serve pour héberger l'app buildée
RUN npm install -g serve

EXPOSE 3000

# Lance le serveur sur le dossier build
CMD ["serve", "-s", "build", "-l", "3000"]
