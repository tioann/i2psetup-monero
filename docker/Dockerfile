FROM phusion/baseimage

CMD ["/sbin/my_init"]

RUN apt-add-repository ppa:i2p-maintainers/i2p -y
RUN apt-get update
RUN apt-get install -y i2p

# Copy over "service" file, this is a modified i2prouter-nowrapper script
# better suited for the phusion docker image.
RUN mkdir -p /etc/service/i2p-router
COPY i2prouter-nowrapper-phusion /etc/service/i2p-router/run
RUN chmod +x /etc/service/i2p-router/run

# Make sure the router console binds to 0.0.0.0 in the container
# so that we can connect to it from the host
RUN sed -i -E 's/(clientApp.0.args=7657)[ \t]+[^ \t]+[ \t]+(.*)/\1 ::,0.0.0.0 \2/' /usr/share/i2p/clients.config

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

