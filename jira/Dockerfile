FROM muicoder/glibc:server-jre

ENV JIRA_VERSION=8.1.0
ENV SERVICEDESK_VERSION=4.1.0

WORKDIR /opt

RUN BASEURL="https://www.atlassian.com/software/jira/downloads/binary" && \
    wget -q ${BASEURL}/atlassian-jira-core-${JIRA_VERSION}.tar.gz && \
    wget -q ${BASEURL}/atlassian-jira-software-${JIRA_VERSION}.tar.gz && \
    wget -q ${BASEURL}/atlassian-servicedesk-${SERVICEDESK_VERSION}.tar.gz && \
    tar -xf atlassian-jira-core-${JIRA_VERSION}.tar.gz && \
    tar -xf atlassian-jira-software-${JIRA_VERSION}.tar.gz && \
    tar -xf atlassian-servicedesk-${SERVICEDESK_VERSION}.tar.gz && \
    mv atlassian-jira-core-*-standalone atlassian && \
\
    mv atlassian-jira-software-*-standalone/atlassian-jira/WEB-INF/application-installation/jira-software-application/* \
       atlassian/atlassian-jira/WEB-INF/atlassian-bundled-plugins && \
    mv atlassian-jira-servicedesk-*-standalone/atlassian-jira/WEB-INF/application-installation/jira-servicedesk-application/* \
       atlassian/atlassian-jira/WEB-INF/atlassian-bundled-plugins && \
    wget -q https://marketplace.atlassian.com/download/plugins/com.atlassian.jira.jira-software-application/ \
        -O atlassian-jira-software-application && mkdir atlassian-jira-software-plugins ; unzip -d atlassian-jira-software-plugins atlassian-jira-software-application && \
    mv -f atlassian-jira-software-plugins/jira-software-application-*.jar \
          atlassian/atlassian-jira/WEB-INF/atlassian-bundled-plugins && \
    mv atlassian/atlassian-jira/WEB-INF/classes/jira-application.properties . && \
    echo "jira.home=/var/atlassian/jira" > atlassian/atlassian-jira/WEB-INF/classes/jira-application.properties && \
\
    rm -rf /opt/atlassian-*

EXPOSE 8080

VOLUME ["/opt/atlassian/logs", "/var/atlassian/jira"]

CMD ["/opt/atlassian/bin/start-jira.sh", "-fg"]
