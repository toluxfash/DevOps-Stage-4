# Build stage
FROM maven:3.8-openjdk-8 as build
WORKDIR /app
# Copy the pom.xml file
COPY pom.xml .
# Download all required dependencies
RUN mvn dependency:go-offline -B
# Copy source code
COPY src ./src
# Build the application
RUN mvn package -DskipTests
# Final stage
FROM openjdk:8-jre-slim
WORKDIR /app
# Copy the built jar file from the build stage
COPY --from=build /app/target/*.jar app.jar
# Set environment variables
ENV SERVER_PORT=8083
ENV JWT_SECRET=${JWT_SECRET}
# Expose port
EXPOSE 8083
# Command to run the application
CMD ["java", "-jar", "app.jar"]