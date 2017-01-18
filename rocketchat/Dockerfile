FROM node:4-slim

# crafted and tuned by pierre@ozoux.net and sing.li@rocket.chat
MAINTAINER buildmaster@rocket.chat

RUN groupadd -r rocketchat \
&&  useradd -r -g rocketchat rocketchat

VOLUME /app/uploads

# gpg: key 4FD08014: public key "Rocket.Chat Buildmaster <buildmaster@rocket.chat>" imported
#RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys 0E163286C20D07B9787EBE9FD7F9D0414FD08104

ENV RC_VERSION 0.49.2

WORKDIR /app

RUN curl -fSL "https://rocket.chat/releases/${RC_VERSION}/download" -o rocket.chat.tgz \
&&  curl -fSL "https://rocket.chat/releases/${RC_VERSION}/asc" -o rocket.chat.tgz.asc \
&&  tar zxvf rocket.chat.tgz \
&&  rm rocket.chat.tgz rocket.chat.tgz.asc \
&&  cd bundle/programs/server \
&&  npm install

#&&  gpg --batch --verify rocket.chat.tgz.asc rocket.chat.tgz \

USER rocketchat

WORKDIR /app/bundle

# needs a mongoinstance - defaults to container linking with alias 'db'
#ENV MONGO_URL=${MONGO_URL} \
#    HOME=/tmp \
#    PORT=3000 \
#    ROOT_URL=http://localhost:3000 \
#    Accounts_AvatarStorePath=/app/uploads

EXPOSE 3000

CMD ["node", "main.js"]
