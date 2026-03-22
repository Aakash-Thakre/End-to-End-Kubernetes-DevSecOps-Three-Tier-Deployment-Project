# ──────────────────────────────────────────────
# Stage 1 – Build
# ──────────────────────────────────────────────
FROM node:18-alpine AS build
 
WORKDIR /app
 
COPY package*.json ./
 
RUN npm install
 
COPY . .
 
ENV NODE_OPTIONS=--openssl-legacy-provider
 
RUN npm run build
 
# ──────────────────────────────────────────────
# Stage 2 – Production (Reduce Image size)
# ──────────────────────────────────────────────
FROM node:18-alpine AS production
 
WORKDIR /app
 
# Only install the tiny static file server
RUN npm install -g serve
 
# Copy ONLY the compiled output from Stage 1
# No source code, no node_modules, no devDependencies
COPY --from=build /app/build ./build
 
EXPOSE 3000
 
CMD ["serve", "-s", "build", "-l", "3000"]
