# Stage 1: Build
FROM node:18-slim AS builder
WORKDIR /app
COPY package.json ./
RUN npm install
RUN npm ci --only=production
COPY . .
RUN npm run build

# Stage 2: Run
FROM node:18-slim
WORKDIR /app
RUN useradd -m nodeuser
USER nodeuser
COPY --from=builder /app .
EXPOSE 3001
CMD ["node", "src/app.js"]