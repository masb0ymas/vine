# Build from repo root: docker build -f apps/vinext-web/Dockerfile -t vinext-web .
FROM node:24-alpine AS build
WORKDIR /repo
RUN corepack enable
COPY . .
RUN pnpm install --frozen-lockfile --filter vinext-web...
RUN pnpm --filter vinext-web build

FROM node:24-alpine
WORKDIR /app
ENV NODE_ENV=production PORT=3000 HOST=0.0.0.0
COPY --from=build /repo/apps/vinext-web/dist/standalone .
USER node
EXPOSE 3000
CMD ["node", "server.js"]
