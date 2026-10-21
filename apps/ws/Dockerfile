FROM oven/bun:1.4.0

WORKDIR /app

COPY package.json bun.lock ./
COPY apps/backend/package.json ./apps/backend/package.json
COPY apps/frontend/package.json ./apps/frontend/package.json
COPY apps/ws/package.json ./apps/ws/package.json
COPY packages/db/package.json ./packages/db/package.json
COPY packages/eslint-config/package.json ./packages/eslint-config/package.json
COPY packages/redis/package.json ./packages/redis/package.json
COPY packages/typescript-config/package.json ./packages/typescript-config/package.json
COPY packages/ui/package.json ./packages/ui/package.json

RUN bun install --frozen-lockfile

COPY apps/ws ./apps/ws
COPY packages/db ./packages/db
COPY packages/redis ./packages/redis

RUN cd packages/db && DATABASE_URL="postgresql://user:pass@localhost:5432/db" bunx prisma generate --schema prisma/schema.prisma

ENV NODE_ENV=production
ENV WS_PORT=5000

EXPOSE 5000

CMD ["bun", "run", "apps/ws/index.ts"]
