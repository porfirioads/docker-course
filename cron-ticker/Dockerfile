FROM node:19.2-alpine3.16 AS deps
WORKDIR /app
COPY package.json ./
RUN npm install

FROM node:19.2-alpine3.16 AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run test
# RUN npm run build

FROM node:19.2-alpine3.16 AS deps-prod
WORKDIR /app
COPY package.json ./
RUN npm install --prod

FROM node:19.2-alpine3.16 AS runner
WORKDIR /app
COPY --from=deps-prod /app/node_modules ./node_modules
COPY app.js ./
COPY tasks ./
CMD [ "node", "app.js" ]
