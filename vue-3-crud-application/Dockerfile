# build stage
FROM node:16-alpine as build-stage
ARG BUILD_ENV=production
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build:${BUILD_ENV}

# runtime stage
FROM node:16-alpine as production-stage
RUN mkdir /app
COPY --from=build-stage /app/dist /app
COPY nginx.conf /etc/nginx/nginx.conf
RUN addgroup --system --gid 1001 fullstack
RUN adduser --system --uid 1001 fullstack
RUN chown -R fullstack:fullstack /app
USER fullstack
