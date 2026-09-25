# Step 1: Build the Java application using Maven
FROM maven:3.8.6-openjdk-8-slim AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Step 2: Run the application on a Tomcat server
FROM tomcat:9.0-jdk8
WORKDIR /usr/local/tomcat

# Remove the default Tomcat applications
RUN rm -rf webapps/*

# Copy the built WAR file from the build stage into Tomcat's webapps directory
COPY --from=build /app/target/dptweb-1.0.war webapps/ROOT.war

# Expose port 8080 (the default for Tomcat)
EXPOSE 8080

# Start Tomcat
CMD ["catalina.sh", "run"]
