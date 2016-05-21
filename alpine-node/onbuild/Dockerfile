FROM asakaguchi/node:6.2
MAINTAINER Akiyoshi Sakaguchi <a-sakaguchi@groovenauts.jp>

ENV SRC /usr/local/src/app

RUN mkdir -p ${SRC}
WORKDIR ${src}

ONBUILD COPY package.json ${SRC}/
ONBUILD RUN npm install
ONBUILD COPY . ${SRC}

EXPOSE 3000

CMD ["npm", "start"]
