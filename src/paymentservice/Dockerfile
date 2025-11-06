FROM --platform=$BUILDPLATFORM node:20.18.1-slim AS builder

# Some packages (e.g. @google-cloud/profiler) require additional
# deps for post-install scripts
RUN apt-get update && apt-get install -y python3 make g++

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install --only=production

FROM node:20.18.1-slim

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app/node_modules ./node_modules
COPY . .

EXPOSE 50051

ENTRYPOINT [ "node", "index.js" ]
