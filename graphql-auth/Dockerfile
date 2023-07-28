#Stage 1
FROM node:14 AS build

WORKDIR /app

COPY package.json ./

RUN npm install -g

COPY . .

RUN npm run build


#Stage 2
FROM node:14-alpine

WORKDIR /app

COPY --from=build /app/package.json /app/package-lock.json ./
COPY --from=build /app/dist ./dist

RUN npm ci --only=production

ENV NODE_ENV=production

CMD ["node", "dist/index.js"]