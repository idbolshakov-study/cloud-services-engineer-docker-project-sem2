FROM node:22-alpine

WORKDIR /app

COPY package*.json ./

ENV NODE_OPTIONS=--openssl-legacy-provider

RUN npm ci

COPY . .

RUN npm run build

RUN addgroup -S frontuser && \
  adduser -S frontuser -G frontuser

RUN chown -R frontuser:frontuser /app
USER frontuser

CMD ["npm", "run", "serve"]

