FROM openjdk:8
LABEL maintainer="GlassOfWhiskey <iacopo.c92@gmail.com>"

WORKDIR /usr/local

ENV LIFERAY_HOME=/usr/local/liferay-ce-portal-7.1-rc1
ENV CATALINA_HOME=$LIFERAY_HOME/tomcat-9.0.6
ENV PATH=$CATALINA_HOME/bin:$PATH
ENV LIFERAY_TOMCAT_URL=https://cdn.lfrs.sl/releases.liferay.com/portal/7.1.0-rc1/liferay-ce-portal-tomcat-7.1-rc1-20180626164228923.zip

RUN apt-get -qq update && \
	apt-get -qq install telnet && \
	apt-get -qq clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
	useradd -ms /bin/bash liferay && \
	set -x && \
  	mkdir -p $LIFERAY_HOME && \
	curl -fSL "$LIFERAY_TOMCAT_URL" -o liferay-ce-portal-tomcat-7.1-rc1-20180626164228923.zip && \
	unzip liferay-ce-portal-tomcat-7.1-rc1-20180626164228923.zip && \
	rm liferay-ce-portal-tomcat-7.1-rc1-20180626164228923.zip && \
	rm -rf $CATALINA_HOME/work/* && \
	chmod 744 $CATALINA_HOME/bin/*.sh && \
	mkdir -p $LIFERAY_HOME/data/document_library && \
	mkdir -p $LIFERAY_HOME/data/elasticsearch/indices

COPY ./configs/setenv.sh $CATALINA_HOME/bin/setenv.sh

RUN chown -R liferay:liferay $LIFERAY_HOME

USER liferay

EXPOSE 8080/tcp

ENTRYPOINT ["catalina.sh", "run"]