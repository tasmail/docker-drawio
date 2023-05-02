FROM node:lts-slim

LABEL maintainer="JGraph Ltd"

ENV RUN_USER            drawio
ENV RUN_GROUP           drawio

RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
        git curl software-properties-common chromium libatk-bridge2.0-0 libgtk-3-0 && \
    apt-add-repository contrib && \
    apt-get update -y && \
    apt-get install -y --no-install-recommends \
        ttf-mscorefonts-installer && \
    mkdir /usr/local/drawio && \
    cd /usr/local/drawio && \
    git clone https://github.com/jgraph/draw-image-export2.git && \
    cd draw-image-export2 && \
    npm install && \
    apt-get remove -y --purge chromium git
    
# Add drawio user
RUN groupadd -r ${RUN_GROUP} && useradd -g ${RUN_GROUP} -d /usr/local/drawio -s /bin/bash ${RUN_USER} && \
    chown -R ${RUN_USER}:${RUN_GROUP} /usr/local/drawio

USER ${RUN_USER}

WORKDIR /usr/local/drawio/draw-image-export2

EXPOSE 8000

CMD ["npm", "start"]