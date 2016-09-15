FROM nginx:latest

RUN apt-get update -y && apt-get install -y \
    unzip \
    openjdk-7-jre \
    wget \
    nginx

WORKDIR /tmp

RUN wget http://cdn.sencha.com/cmd/6.1.3/no-jre/SenchaCmd-6.1.3-linux-amd64.sh.zip
RUN unzip SenchaCmd-6.1.3-linux-amd64.sh.zip
COPY conf/senchacmd.varfile /tmp/senchacmd.varfile

RUN /tmp/`find SenchaCmd*.sh` -q -varfile /tmp/senchacmd.varfile -dir "/opt/sencha"
RUN ln -s /opt/sencha/sencha /usr/local/bin/sencha

COPY src /opt/demo
WORKDIR /opt/demo
RUN sencha app build
RUN cp -r build/production/demo/* /usr/share/nginx/html
