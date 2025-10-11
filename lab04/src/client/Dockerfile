FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci --no-audit --no-fund
COPY . .
ENV CI=true
ENV NODE_OPTIONS=--openssl-legacy-provider
RUN npm run build

FROM nginx:1.27-alpine
COPY --from=build /app/build/ /usr/share/nginx/html/
EXPOSE 80
HEALTHCHECK --interval=30s --timeout=3s CMD wget -qO- http://127.0.0.1/ || exit 1
LABEL org.opencontainers.image.title="lab04-client" \
      org.opencontainers.image.part-of="lab04" \
      org.opencontainers.image.component="client"
