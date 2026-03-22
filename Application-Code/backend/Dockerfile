# ──────────────────────────────────────────────
# Stage 1 – Install all deps + copy source
# ──────────────────────────────────────────────

FROM node:18-alpine AS build
 
WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .


# ──────────────────────────────────────────────
# Stage 2 – Production 
# ──────────────────────────────────────────────

FROM node:18-alpine AS production

WORKDIR /app

COPY package*.json ./

RUN npm install --omit=dev

COPY --from=build /app .

EXPOSE 3500

CMD ["node", "index.js"]