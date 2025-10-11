FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --no-audit --no-fund
COPY . .
ENV PORT=4000
EXPOSE 4000
HEALTHCHECK --interval=30s --timeout=3s CMD wget -qO- http://127.0.0.1:4000/api/users || exit 1
CMD ["node", "./bin/www"]
LABEL org.opencontainers.image.title="lab04-server" \
      org.opencontainers.image.part-of="lab04" \
      org.opencontainers.image.component="server"
