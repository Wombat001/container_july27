FROM mysql:5.7
ENV MYSQL_ROOT_PASSWORD=changeit MYSQL_PORT=3306 MYSQL_DB_PATH=/var/lib/mysql 

# copy SQL files to 
ADD 0-northwind-default-current-timestamp.sql /docker-entrypoint-initdb.d
ADD 1-northwind-data.sql /docker-entrypoint-initdb.d
#ADD main.js .
#ADD package.json .
#ADD package-lock.json .
#ADD public public
#ADD views views
# add Healthcheck 
HEALTHCHECK --interval=3s --timeout=3s --start-period=5s --retries=3 cmd mysqladmin ping -uroot -p ${MYSQL_ROOT_PASSWORD} //exit 1

EXPOSE ${MYSQL_PORT}
VOLUME ${MYSQL_DB_PATH}