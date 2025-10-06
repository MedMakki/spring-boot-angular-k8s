# Étape 1 : Build Angular avec Node.js
FROM node:18 AS build
WORKDIR /app

# Copier les fichiers package.json pour installer les dépendances
COPY package*.json ./
RUN npm install

# Copier tout le projet et builder l'app
COPY . .
RUN npm run build --prod

# Étape 2 : Servir avec Nginx
FROM nginx:alpine
COPY --from=build /app/dist/angular-17-client /usr/share/nginx/html

# Exposer le port
EXPOSE 80

# Lancer Nginx
CMD ["nginx", "-g", "daemon off;"]
