FROM mariadb:latest

ENV MYSQL_DATABASE=student_db
ENV MYSQL_USER=admin
ENV MYSQL_PASSWORD=

COPY init.sql /docker-entrypoint-initdb.d/
