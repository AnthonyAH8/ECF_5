FROM node:12-alpine AS build

WORKDIR /app

RUN apk add --no-cache make gcc g++ python2

COPY package.json ./

RUN npm install

COPY . .

RUN npm run build

FROM node:12-alpine

WORKDIR /app

COPY package.json ./

RUN npm install --only=production

COPY --from=build /app/build ./build
COPY server.js ./

EXPOSE 3000

CMD ["node", "server.js"]
