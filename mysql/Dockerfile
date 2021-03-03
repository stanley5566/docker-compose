FROM mysql:5.6
COPY ./setup.sql /docker-entrypoint-initdb.d/
RUN chmod 777 /docker-entrypoint-initdb.d/setup.sql
