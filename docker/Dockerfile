FROM jenkins/jenkins:lts-windowsservercore-1809

# Set Maven environment variables
ENV M2_HOME='C:\Program Files\apache-maven-3.8.6'
ENV PATH='%PATH%;%M2_HOME%\bin'

# Add Jenkins user to Docker group
RUN net localgroup "Docker Desktop Users" "jenkins" /add

# Install Jenkins plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Set Jenkins configuration
COPY jenkins.yaml /usr/share/jenkins/ref/jenkins.yaml

# Set Jenkins jobs
COPY jobs /usr/share/jenkins/ref/jobs/

# Set Jenkins user configuration
COPY userContent /usr/share/jenkins/ref/userContent/

# Set Jenkins credentials
COPY credentials.xml /usr/share/jenkins/ref/credentials.xml

# Set Jenkins script console scripts
COPY script-console /usr/share/jenkins/ref/script-console/


# FROM openjdk:11-jre as builder
# WORKDIR application
# ARG ARTIFACT_NAME
# COPY ${ARTIFACT_NAME}.jar application.jar
# RUN java -Djarmode=layertools -jar application.jar extract

# # Download dockerize and cache that layer
# ARG DOCKERIZE_VERSION
# RUN wget -O dockerize.tar.gz https://github.com/jwilder/dockerize/releases/download/${DOCKERIZE_VERSION}/dockerize-alpine-linux-amd64-${DOCKERIZE_VERSION}.tar.gz
# RUN tar xzf dockerize.tar.gz
# RUN chmod +x dockerize


# # wget is not installed on adoptopenjdk:11-jre-hotspot
# FROM adoptopenjdk:11-jre-hotspot

# WORKDIR application

# # Dockerize
# COPY --from=builder application/dockerize ./

# ARG EXPOSED_PORT
# EXPOSE ${EXPOSED_PORT}

# ENV SPRING_PROFILES_ACTIVE docker

# COPY --from=builder application/dependencies/ ./
# COPY --from=builder application/spring-boot-loader/ ./
# COPY --from=builder application/snapshot-dependencies/ ./
# COPY --from=builder application/application/ ./
# ENTRYPOINT ["java", "org.springframework.boot.loader.JarLauncher"]
