ARG ZULU_VERSION
FROM azul/zulu-openjdk-centos:$ZULU_VERSION

LABEL maintainer="qaware-oss@qaware.de"

ENV PAYARA_PATH /opt/payara

RUN yum -q -y install wget && \
 mkdir -p $PAYARA_PATH/deployments && \
 mkdir -p $PAYARA_PATH/libs && \
 adduser payara && echo payara:payara | chpasswd && \
 chown -R payara:payara /opt

ARG PAYARA_TAG
ARG PAYARA_RELEASE

ENV PAYARA_PKG https://search.maven.org/remotecontent?filepath=fish/payara/extras/payara-micro/$PAYARA_TAG/payara-micro-$PAYARA_TAG.jar
ENV PAYARA_VERSION $PAYARA_RELEASE
ENV PKG_FILE_NAME payara-micro.jar

RUN wget --quiet -O $PAYARA_PATH/$PKG_FILE_NAME $PAYARA_PKG

ENV DEPLOY_DIR $PAYARA_PATH/deployments
ENV AUTODEPLOY_DIR $PAYARA_PATH/deployments
ENV PAYARA_MICRO_JAR=$PAYARA_PATH/$PKG_FILE_NAME

# Default payara ports to expose
EXPOSE 8080 8181 8443 6900

USER payara
WORKDIR $PAYARA_PATH

ENTRYPOINT ["java", "--add-modules", "java.se.ee", "-server", "-XX:ThreadStackSize=256", "-XX:MaxMetaspaceSize=128m", "-XX:+UseG1GC", "-XX:+UseStringDeduplication", "-jar", "/opt/payara/payara-micro.jar"]
CMD ["--deploymentDir", "/opt/payara/deployments"]
