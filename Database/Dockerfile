FROM mariadb:latest

ENV MYSQL_DATABASE=student_db
ENV MYSQL_USER=linux
ENV MYSQL_PASSWORD=redhat

COPY init.sql /docker-entrypoint-initdb.d/

# Expose MariaDB port
EXPOSE 3306


FROM mariadb:latest

# Set environment variables for MariaDB
ENV MYSQL_ROOT_PASSWORD=rootpassword  # Set the root password here
ENV MYSQL_DATABASE=student_db
ENV MYSQL_USER=admin
ENV MYSQL_PASSWORD=adminpassword

# Copy the initialization script (optional)
COPY init.sql /docker-entrypoint-initdb.d/

# Expose MariaDB port
EXPOSE 3306
