FROM mariadb:latest

ENV MYSQL_DATABASE=student_db
ENV MYSQL_USER=linux
ENV MYSQL_PASSWORD=redhat

COPY init.sql /docker-entrypoint-initdb.d/

# Expose MariaDB port
EXPOSE 3306