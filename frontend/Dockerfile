FROM node:22.6-bookworm AS builder

RUN git clone https://github.com/kanban-org/kanban-board.git

RUN sed -i "s/'0.0.0.0'/process.env.DB_PROD_HOST/g" /kanban-board/kanban-server/src/config/config.js

WORKDIR /kanban-board

RUN npm install && CI=false npm run build:client && CI=false npm run build:server

FROM nginx:1.27.0-alpine3.19-slim

COPY --from=builder /kanban-board /kanban-board

#ENTRYPOINT [ "/bin/bash" ]