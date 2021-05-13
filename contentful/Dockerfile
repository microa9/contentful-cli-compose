FROM ubuntu:20.04

ENV TZ=Asia/Tokyo
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && echo ${TZ} > /etc/timezone

RUN apt-get update \
    && apt-get install -y nodejs npm git

RUN npm install -g contentful-cli

WORKDIR /var/www/html
RUN git clone https://github.com/contentful/starter-gatsby-blog.git

WORKDIR /var/www/html/starter-gatsby-blog

ARG CONTENTFUL_MANAGEMENT_TOKEN
ARG CONTENTFUL_SPACE_ID
ARG CONTENTFUL_ACCESS_TOKEN

RUN npm install \
    && npm run setup -- \
        --managementToken=${CONTENTFUL_MANAGEMENT_TOKEN} \
        --spaceId=${CONTENTFUL_SPACE_ID} \
        --accessToken=${CONTENTFUL_ACCESS_TOKEN}

ARG CONTENTFUL_DEVELOP_PORT=3000
ENV CONTENTFUL_DEVELOP_PORT ${CONTENTFUL_DEVELOP_PORT}

CMD ["npm", "run", "dev", "--", "-H", "0.0.0.0", "-p", "${CONTENTFUL_DEVELOP_PORT}"]
