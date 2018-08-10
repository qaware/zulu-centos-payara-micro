FROM azul/zulu-openjdk-centos:8u181

LABEL maintainer="qaware-oss@qaware.de"

ENV PAYARA_PATH /opt/payara

RUN yum -q -y install curl && \
 update-ca-trust && \
 useradd -d $PAYARA_PATH payara && echo payara:0 | chpasswd && \
 mkdir -p $PAYARA_PATH/deployments && \
 mkdir -p $PAYARA_PATH/libs && \
 chown -R payara:0 $PAYARA_PATH && \
 echo "export PS1='> '" >> /etc/bash.bashrc && \
 echo "alias ll='ls -al'" >> /etc/bash.bashrc

ENV PAYARA_PKG https://search.maven.org/remotecontent?filepath=fish/payara/extras/payara-micro/4.1.2.181/payara-micro-4.1.2.181.jar
ENV PAYARA_VERSION 4.181
ENV PKG_FILE_NAME payara-micro.jar

USER payara
WORKDIR $PAYARA_PATH

RUN curl --silent --show-error --output $PAYARA_PATH/$PKG_FILE_NAME $PAYARA_PKG

ENV DEPLOY_DIR $PAYARA_PATH/deployments
ENV AUTODEPLOY_DIR $PAYARA_PATH/deployments
ENV PAYARA_MICRO_JAR=$PAYARA_PATH/$PKG_FILE_NAME

# Default payara ports to expose
EXPOSE 8080 8081 8443 5701 5900

ENTRYPOINT ["java", "-server", "-XX:+UnlockExperimentalVMOptions", "-XX:+UseCGroupMemoryLimitForHeap", "-XX:MaxRAMFraction=3", "-XX:ThreadStackSize=256", "-XX:MaxMetaspaceSize=128m", "-XX:+UseG1GC", "-XX:ParallelGCThreads=2", "-XX:CICompilerCount=2", "-XX:+UseStringDeduplication", "-jar", "/opt/payara/payara-micro.jar"]
CMD ["--deploymentDir", "/opt/payara/deployments"]
