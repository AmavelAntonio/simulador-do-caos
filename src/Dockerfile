FROM node:20.9.0 AS build
WORKDIR /app
COPY package*.json .
RUN npm install
COPY . .
RUN npm run compile

FROM  node:20.9.0-alpine
WORKDIR /app
RUN apk add --no-cache stress-ng
COPY --from=build /app/views /app/views
COPY --from=build /app/dist ./dist
COPY --from=build /app/node_modules ./node_modules
COPY --from=build /app/package.json ./
EXPOSE 3000
CMD [ "npm", "start" ]
