FROM node:20-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

ARG VITE_APP_API_ENDPOINT_URL
ARG VITE_APP_TMDB_V3_API_KEY
ENV VITE_APP_API_ENDPOINT_URL=$VITE_APP_API_ENDPOINT_URL
ENV VITE_APP_TMDB_V3_API_KEY=$VITE_APP_TMDB_V3_API_KEY

RUN npx vite build

FROM nginx:alpine

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
