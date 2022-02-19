FROM registry.nexdev.net:5050/docker/haproxy/haproxy-debian:2.4-test
ARG ENV
RUN mkdir -p /root/.ssh/
ADD dockerfiles/rsa /root/.ssh/
RUN chmod -R 600 /root/.ssh/
RUN ssh-keyscan -t rsa git3.nexdev.net >> /root/.ssh/known_hosts
RUN ls -l /root/.ssh/
RUN cat /root/.ssh/id_rsa
RUN cd /srv/ && git clone git@git3.nexdev.net:haproxy/haproxy-default.git
RUN ls -l /srv/
#############
COPY configs/$ENV /usr/local/etc/haproxy/configs/$ENV
RUN ls -l /srv/haproxy-default/configs
RUN ls -l /srv/haproxy-default/configs/$ENV/
RUN cp /srv/haproxy-default/configs/$ENV/00-global-defaults.cfg /usr/local/etc/haproxy/configs/$ENV/
RUN ls /usr/local/etc/haproxy/configs/$ENV
RUN cat /usr/local/etc/haproxy/configs/$ENV/*.cfg > /usr/local/etc/haproxy/configs/$ENV/haproxy.cfg.tmp
RUN cp /usr/local/etc/haproxy/configs/$ENV/haproxy.cfg.tmp /usr/local/etc/haproxy/haproxy.cfg
RUN cp /srv/haproxy-default/whitelisted.ips /etc/haproxy/whitelisted.ips
RUN cp /srv/haproxy-default/certs/lumigame.com.pem /etc/haproxy/lumigame.com.pem
RUN mkdir /usr/local/etc/haproxy/maps
RUN cat /usr/local/etc/haproxy/configs/$ENV/maps/*.map > /usr/local/etc/haproxy/maps/hosts.map
RUN cat /usr/local/etc/haproxy/haproxy.cfg
RUN cat /etc/haproxy/maps/hosts.map