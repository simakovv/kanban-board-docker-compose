FROM node:22.6-bookworm AS builder

RUN git clone https://github.com/kanban-org/kanban-board.git

RUN sed -i "s/'0.0.0.0'/process.env.DB_PROD_HOST/g" /kanban-board/kanban-server/src/config/config.js

WORKDIR /kanban-board

RUN npm install && CI=false npm run build:client && CI=false npm run build:server

FROM node:22.6-bookworm

COPY --from=builder /kanban-board /kanban-board

WORKDIR /kanban-board

ENTRYPOINT [ "npm", "run", "start", "--workspace=kanban-server" ]
#ENTRYPOINT [ "/bin/bash" ]