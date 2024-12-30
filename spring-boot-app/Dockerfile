# # You can change this base image to anything else
# # But make sure to use the correct version of Java
# #FROM adoptopenjdk/openjdk11:alpine-jre
# FROM eclipse-temurin:11-jre

# # Simply the artifact path
# ARG artifact=target/spring-boot-web.jar

# WORKDIR /opt/app

# COPY ${artifact} app.jar

# # This should not be changed
# ENTRYPOINT ["java","-jar","app.jar"]


# Use Eclipse Temurin JRE image to build the application
FROM eclipse-temurin:11-jre AS build

# Set the artifact path
ARG artifact=target/spring-boot-web.jar

# Copy the built JAR file into the image
WORKDIR /opt/app
COPY ${artifact} app.jar

# Use distroless base image for the final image
FROM gcr.io/distroless/java:11

# Set the working directory inside the distroless image
WORKDIR /opt/app

# Copy the JAR file from the build stage
COPY --from=build /opt/app/app.jar .

# Set the entrypoint to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
