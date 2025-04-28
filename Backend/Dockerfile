# Use an official Java runtime as a parent image
FROM openjdk:17-jdk-slim

# Set the working directory inside the container
WORKDIR /app

# Clone the repository and install necessary dependencies
RUN apt-get update && \
    apt-get install -y git maven && \
    git clone https://github.com/rajatpzade/cloudblitz-student-app.git /app && \
    cd /app/backend && \
    mvn clean package

# Set the environment variables for the database connection
ENV DB_URL=jdbc:mariadb://172.17.0.2:3306/student_db
ENV DB_USERNAME=linux
ENV DB_PASSWORD=redhat

# Expose port for the backend application
EXPOSE 8080

# Run the backend application
CMD ["java", "-jar", "/app/backend/target/student-registration-backend-0.0.1-SNAPSHOT.jar"]
