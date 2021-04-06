#FROM openjdk:8-jdk-alpine as build
FROM gradle:6.8.3-jdk8 AS build
COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src
#RUN gradle build -stacktrace --no-daemon
RUN gradle build -b ./gradle.build --no-daemon
#RUN ./gradlew bootWar
RUN ls -la ./build/libs
#VOLUME /output /build/libs
#RUN cp ./build/libs/*.war libOutput/spring-boot-application.war

#FROM openjdk:8-jdk-alpine
FROM tomcat:8.5.64-jdk8-corretto
run mkdir /app
COPY --from=build /home/gradle/src/build/libs/*.war /user/local/tomcat/webapps/spring-boot-application.war
#VOLUME /user/local/tomcat/webapps
##COPY /libOutput/*.war /user/local/tomcat/webapps/spring-boot-application.war
RUN ls -la /user/local/tomcat/webapps 
CMD ["catalina.sh", "run"]
