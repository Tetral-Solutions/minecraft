# Copied & Edited from https://github.com/CivMC/CivDocker/blob/master/paper/Dockerfile

FROM itzg/minecraft-server:java17

RUN useradd minecraft
USER minecraft:minecraft

# https://github.com/itzg/docker-minecraft-server/blob/master/README.md#versions
ENV VERSION=latest

# Before this next step, we're not going to copy our own JARs of plugins we're not maintaining ourselves. 
# https://github.com/itzg/docker-minecraft-server#auto-downloading-spigotmcbukkitpapermc-plugins
# COPY plugins /plugins
# We have none of our own plugins to install, so skip this step. Download these base plugins from SpigotMC using SPIGET_RESOURCES
ENV SPIGET_RESOURCES=19254,27448,25391,102902 
# FIXME: We should probably hold onto a stable long-term build from an older version, and just provide upwards forward-compatibility to all future versions
#ViaVersion, ViaBackwards, VoidGen, NoEncryption
ENV REMOVE_OLD_MODS=TRUE

# https://github.com/itzg/docker-minecraft-server#optional-plugins-mods-and-config-attach-points
COPY config /config
ENV COPY_CONFIG_DEST=/data
ENV SYNC_SKIP_NEWER_IN_DESTINATION=false
# Really confusing, but paper configs (since 1.19) now need to go in their OWN config directory.
RUN mkdir config && mv paper*.yml config

# https://github.com/itzg/docker-minecraft-server#running-a-paper-server
ENV TYPE=PAPER
ENV EULA=TRUE
ENV USE_AIKAR_FLAGS=TRUE
# https://github.com/itzg/docker-minecraft-server#replacing-variables-inside-configs
ENV REPLACE_ENV_VARIABLES=TRUE
ENV REPLACE_ENV_DURING_SYNC=TRUE

ENV CFG_FORWARDING_SECRET_FILE=/run/secrets/forwarding_secret