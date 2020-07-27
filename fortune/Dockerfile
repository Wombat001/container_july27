FROM node:latest

ENV APP_DIR=/app APP_PORT=3000

WORKDIR ${APP_DIR}

ADD main.js .
ADD package.json .
ADD package-lock.json .
ADD public public
ADD views views
RUN npm install

# Running the image
# Add health check
        HEALTHCHECK --interval=3s --timeout=3s --start-period=5s --retries=3 cmd curl -s -f http://localhost:${APP_PORT}/health > /dev/null || exit 1
EXPOSE ${APP_PORT}

ENTRYPOINT [ "node", "main.js" ]

# CMD [ "${APP_PORT}" ]

