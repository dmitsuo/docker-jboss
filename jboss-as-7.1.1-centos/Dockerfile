FROM davimss/docker-jdk:8

ENV JBOSS_VERSION jboss-as-7.1.1.Final
ENV JBOSS_HOME /opt/$JBOSS_VERSION
ENV PATH $JBOSS_HOME/bin:$PATH
ENV JBOSS_DOWN_FILE $JBOSS_VERSION.tar.gz
ENV JBOSS_BASE_DOWNLOAD_URL https://www.dropbox.com/s/223edmwexm72x6u
ENV JBOSS_DOWNLOAD_URL ${JBOSS_BASE_DOWNLOAD_URL}/${JBOSS_DOWN_FILE}?dl=1
ENV JBOSS_DEPLOY_DIR ${JBOSS_HOME}/standalone/deployments
ENV JBOSS_CONFIG_DIR ${JBOSS_HOME}/standalone/configuration
ENV JBOSS_LOG_DIR ${JBOSS_HOME}/standalone/log

RUN set -x ; \
    mkdir -p $JBOSS_HOME ; \
    cd $JBOSS_HOME ; \
    curl -o $JBOSS_HOME/$JBOSS_DOWN_FILE -L $JBOSS_DOWNLOAD_URL ; \
    tar -xvf $JBOSS_DOWN_FILE --strip-components=1 ; \
    rm -rf bin/*.bat ; \
    rm -rf bin/*.ps1 ; \
    rm -rf $JBOSS_DOWN_FILE ; \
    echo -e "\nJAVA_OPTS=\"\$JAVA_OPTS -Duser.language=pt -Duser.country=BR -Duser.timezone=America/Belem\"" >> $JBOSS_HOME/bin/standalone.conf ; \
    ln -s $JBOSS_HOME /opt/jboss

WORKDIR $JBOSS_HOME

COPY standalone.xml ${JBOSS_CONFIG_DIR}
COPY ojdbc6-11.2.0.3.0.jar ${JBOSS_DEPLOY_DIR}

# EXPOSE 8080 8443

#CMD bin/standalone.sh -b=0.0.0.0 -bmanagement=0.0.0.0
CMD bin/standalone.sh -b=0.0.0.0