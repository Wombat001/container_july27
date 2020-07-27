FROM node:14

# env variables
# for application
ENV APP_DIR=/app APP_PORT=3000

ENV DB_USER=root DB_PASSWORD=changit

WORKDIR ${APP_DIR}

ADD main.js .
ADD package.json .
ADD package-lock.json .

ADD config config
ADD public public
ADD views views

run npm install

# Add health check
HEALTHCHECK --interval=3s --timeout=3s --start-period=5s --retries=3 CMD curl -s -f http://localhost:${APP_PORT}/health || exit 1

EXPOSE ${APP_PORT}

ENTRYPOINT [ "node", "main.js" ]



