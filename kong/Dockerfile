FROM kong:2.0.0

RUN apt -y update && apt -y install curl

# get ContainerPilot release
ENV CONTAINERPILOT_VERSION 3.0.0
RUN export checksum=6da4a4ab3dd92d8fd009cdb81a4d4002a90c8b7c \
    && curl -Lso /tmp/containerpilot.tar.gz \
         "https://github.com/joyent/containerpilot/releases/download/${CONTAINERPILOT_VERSION}/containerpilot-${CONTAINERPILOT_VERSION}.tar.gz" \
    && echo "${checksum}  /tmp/containerpilot.tar.gz" | sha1sum -c \
    && tar zxf /tmp/containerpilot.tar.gz -C /usr/local/bin \
    && rm /tmp/containerpilot.tar.gz

RUN apt -y install procps

# add config file
COPY containerpilot.json /etc/containerpilot.json
ENV CONTAINERPILOT=/etc/containerpilot.json

EXPOSE 8000 8443 8001 7946

ENTRYPOINT ["/usr/local/bin/containerpilot"]
