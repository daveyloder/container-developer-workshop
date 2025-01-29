FROM openjdk:11.0-jdk

WORKDIR /app

# Copy the maven wrapper files first
COPY .mvn/ .mvn/
COPY mvnw mvnw
COPY pom.xml pom.xml

# Debug: List files and check mvnw exists
RUN ls -la && \
    # Make mvnw executable
    chmod +x mvnw && \
    # Verify it's executable
    ls -la mvnw

# Download dependencies separately (better layer caching)
RUN ./mvnw dependency:go-offline

# Then copy the source code
COPY src/ src/

# Debug: List all files
RUN ls -la

# Build the application
RUN ./mvnw clean compile assembly:single

# Run the jar
CMD ["java", "-jar", "target/sample-app-1.0.0-jar-with-dependencies.jar"]
