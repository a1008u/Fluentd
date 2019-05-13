FROM ubuntu:xenial

RUN apt-get update && apt-get -y upgrade
RUN apt-get install sudo
RUN apt-get install -y curl
RUN apt-get install -y vim
RUN apt-get install -y git

#デフォルトで24224を使うのでポートを空けておく
EXPOSE 24224

# fluentd(td-agent)のインストール
RUN curl -L https://toolbelt.treasuredata.com/sh/install-ubuntu-xenial-td-agent3.sh | sh

# python2.7
RUN apt-get -y install python2.7
RUN apt install -y python-pip python-dev

# GCPのダウンロード
RUN curl https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz > /tmp/google-cloud-sdk.tar.gz

# パッケージのダウンロード
RUN mkdir -p /usr/local/gcloud \
  && tar -C /usr/local/gcloud -xvf /tmp/google-cloud-sdk.tar.gz \
  && /usr/local/gcloud/google-cloud-sdk/install.sh

# パスを通す
ENV PATH $PATH:/usr/local/gcloud/google-cloud-sdk/bin

# fluentd-plugin-bigqueryのインストール
RUN /opt/td-agent/embedded/bin/fluent-gem install --no-document specific_install
RUN /opt/td-agent/embedded/bin/fluent-gem specific_install https://github.com/kaizenplatform/fluent-plugin-bigquery.git