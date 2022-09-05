# Copied & Edited from https://github.com/CivMC/CivDocker/blob/master/waterfall/Dockerfile

FROM itzg/bungeecord:java17

# https://github.com/itzg/docker-bungeecord/#optional-environment-settings
ENV VELOCITY_VERSION=latest

ENV SPIGET_PLUGINS=19254,27448
#ViaVersion, ViaBackwards

# https://github.com/itzg/docker-bungeecord#volumes
COPY config /config

ENV TYPE=VELOCITY
ENV JVM_XX_OPTS="-XX:+UseG1GC -XX:G1HeapRegionSize=4M -XX:+UnlockExperimentalVMOptions -XX:+ParallelRefProcEnabled -XX:+AlwaysPreTouch -XX:MaxInlineLevel=15"

# https://github.com/itzg/docker-bungeecord#volumes
# https://github.com/itzg/docker-bungeecord#bungeecord-configuration
ENV REPLACE_ENV_VARIABLES=TRUE
ENV REPLACE_ENV_DURING_SYNC=TRUE

ENV CFG_FORWARDING_SECRET_FILE=/run/secrets/forwarding_secret

RUN useradd minecraft || echo "User already exists, skipping"
RUN mkdir /data || echo "/data already exists, skipping"
RUN chown -R 1002:1003 /data
USER minecraft