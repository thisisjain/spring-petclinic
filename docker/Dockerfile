FROM openjdk:11
EXPOSE 8070
ENV APP_HOME /usr/src/app
COPY /var/lib/jenkins/workspace/pipeline/target/spring-petclinic-2.7.3.jar $APP_HOME/app.jar
WORKDIR $APP_HOME
ENTRYPOINT exec java -jar app.jar
