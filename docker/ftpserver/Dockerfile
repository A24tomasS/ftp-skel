FROM debian:13

RUN apt update  && apt install -y \
    procps \
    iproute2 \
    iputils-ping \
    vsftpd \
    dnsutils \
    rsyslog \
    passwd \
    && rm -rf /var/lib/apt/lists/*

# Crear usuarios con home e pass "a"
RUN for u in gandalf saruman aragorn frodo; do \
        useradd -m "$u" && \
        echo "$u:a" | chpasswd ; \
    done

COPY entrypoint.sh /sbin
RUN mkdir /sauron
RUN chmod 666 /sauron
RUN chmod a+x /sbin/entrypoint.sh

RUN sed -i 's/^\s*module(load="imklog")/#module(load="imklog")/' /etc/rsyslog.conf

ENTRYPOINT ["/sbin/entrypoint.sh"]
