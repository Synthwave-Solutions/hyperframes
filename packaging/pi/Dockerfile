FROM node:24.18.0-bookworm-slim
RUN apt-get update && apt-get install -y --no-install-recommends chromium ffmpeg ca-certificates tini && rm -rf /var/lib/apt/lists/*
COPY . /opt/hyperframes
RUN chmod +x /opt/hyperframes/packages/cli/bin/*.mjs && ln -s /opt/hyperframes/packages/cli/bin/hyperframes.mjs /usr/local/bin/hyperframes
USER node
WORKDIR /workspace
ENV PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium
EXPOSE 5227
ENTRYPOINT ["tini", "--", "hyperframes"]
CMD ["preview", "/workspace", "--port", "5227", "--foreground", "--no-open"]
