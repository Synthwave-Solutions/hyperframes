FROM oven/bun:1.3.11 AS build
WORKDIR /src
COPY . .
RUN bun install --frozen-lockfile && bun run build
FROM node:24.18.0-bookworm-slim
RUN apt-get update && apt-get install -y --no-install-recommends chromium ffmpeg ca-certificates tini && rm -rf /var/lib/apt/lists/*
COPY --from=build /src /opt/hyperframes
RUN ln -s /opt/hyperframes/packages/cli/bin/hyperframes.mjs /usr/local/bin/hyperframes
USER node
WORKDIR /workspace
ENV PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium
EXPOSE 5227
ENTRYPOINT ["tini", "--", "hyperframes"]
CMD ["preview", "/workspace", "--port", "5227", "--foreground", "--no-open"]
