FROM debian:13

RUN apt update  && apt install -y \
    procps \
    iproute2 \
    iputils-ping \
    vsftpd \
    dnsutils \
    rsyslog \
    passwd \
    openssl \
    && rm -rf /var/lib/apt/lists/*

# Crear usuarios con home e pass "a"
RUN for u in gandalf saruman aragorn frodo; do \
        useradd -m "$u" && \
        echo "$u:a" | chpasswd; \
        chmod 555 /home/$u; \
        chmod 555 /home/$u/*; \
        mkdir /home/$u/public_html; \
        chmod 755 /home/$u/*; \
        chown $u /home/$u/public_html; \
    done

COPY entrypoint.sh /sbin
RUN mkdir /sauron
RUN mkdir /sauron/public_upload
RUN chmod 555 /sauron
RUN chmod 777 /sauron/public_upload
RUN chmod a+x /sbin/entrypoint.sh

#RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/vsftpd.pem -out /etc/ssl/certs/vsftpd.pem

RUN sed -i 's/^\s*module(load="imklog")/#module(load="imklog")/' /etc/rsyslog.conf

ENTRYPOINT ["/sbin/entrypoint.sh"]
