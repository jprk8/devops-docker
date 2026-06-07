FROM ubuntu:24.04

WORKDIR /usr/src/app

RUN apt-get update && apt-get install -y curl && \
    curl -fsSL https://deb.nodesource.com/setup_16.x | bash - && \
    apt-get install -y nodejs && \
    apt-get purge -y --auto-remove curl && \
    rm -rf /var/lib/apt/lists/*

# Copy package.json for npm
COPY package*.json ./
RUN npm install

COPY . .

ENV REACT_APP_BACKEND_URL=http://localhost:8000/api

RUN npm run build && \
    rm -rf src public node_modules package*.json && \
    npm cache clean --force

RUN npm install -g serve && \
    useradd -m appuser

USER appuser

EXPOSE 5001

CMD ["serve", "-s", "-l", "5001", "build"]
