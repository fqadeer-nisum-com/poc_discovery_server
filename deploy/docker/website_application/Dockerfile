FROM openjdk:8-jre-alpine

# Initializing variables that will be used later.
ENV APP_NAME=website_application
ENV SERVER_PORT=9001
ENV JAR_FILE=website-application-SNAPSHOT.jar


# Copy all the required files/directories
COPY ${APP_NAME}/${JAR_FILE} /usr/src/${JAR_FILE}

# Startup Command
ENTRYPOINT java -Dserver.port=${SERVER_PORT} -Deureka.client.serviceUrl.defaultZone=http://$(ping -c1 discovery_server |  grep 'bytes from 172' | cut -d' ' -f 4 | cut -d: -f 1):7001/eureka/ -Dadmin-application.url=http://$(ping -c1 website_application |  grep 'bytes from 172' | cut -d' ' -f 4 | cut -d: -f 1):9001/admin/companies -Dnews-application.url=http://$(ping -c1 website_application |  grep 'bytes from 172' | cut -d' ' -f 4 | cut -d: -f 1):9001/news/twitter -jar /usr/src/${JAR_FILE}
