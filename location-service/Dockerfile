# Use Maven to build the project
FROM maven:3.8.5-openjdk-17 AS build

WORKDIR /app

# Copy the pom.xml and download dependencies
COPY pom.xml ./
RUN mvn dependency:go-offline -B

# Copy the rest of the project files
COPY src ./src

# Build the project
RUN mvn clean package -DskipTests

# Use OpenJDK for the final image
FROM openjdk:17-jdk-alpine

WORKDIR /app

# Copy JAR file from the build stage
COPY --from=build /app/target/location-service-0.0.1-SNAPSHOT.jar location-service.jar

# Run the application
ENTRYPOINT ["java", "-jar", "location-service.jar"]
