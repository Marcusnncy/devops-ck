# ---------- Stage 1: Build ----------
FROM node:20-alpine AS build
WORKDIR /app

# Only install dependencies first
COPY package*.json ./
RUN npm install

# Receive CI/CD environment variable
ARG VITE_API_BASE_URL
ENV VITE_API_BASE_URL=${VITE_API_BASE_URL}

# Copy source code
COPY . .

# Build Vite app
RUN npm run build

# ---------- Stage 2: Serve with Nginx ----------
FROM nginx:1.27-alpine

COPY --from=build /app/dist /usr/share/nginx/html

# Optional: custom nginx config
# COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
