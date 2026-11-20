FROM node:20-alpine

ENV NODE_ENV=production \
    PORT=5000

WORKDIR /app

COPY --chown=node:node package*.json ./
RUN npm install --omit=dev --ignore-scripts --no-audit --no-fund \
    && npm cache clean --force

COPY --chown=node:node src/ ./src

USER node

EXPOSE 5000

HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
    CMD wget -q -O /dev/null http://127.0.0.1:5000/health || exit 1

CMD ["npm", "start"]