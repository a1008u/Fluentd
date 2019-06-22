FROM golang:alpine

USER root
RUN apk update && apk add python \
    python-dev  \
		make  \
		gcc  \
		sudo \
		curl \
		vim \
		git \
		g++  \
		ruby-dev \
		libc-dev  \
    tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    apk del tzdata && \
    rm -rf /var/cache/apk/*

ENV PYTHON_PIP_VERSION 19.1.1

# # GCPのダウンロード
RUN curl https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz > /tmp/google-cloud-sdk.tar.gz

# パッケージのダウンロード
RUN mkdir -p /usr/local/gcloud \
  && tar -C /usr/local/gcloud -xvf /tmp/google-cloud-sdk.tar.gz \
  && /usr/local/gcloud/google-cloud-sdk/install.sh

# パスを通す
ENV PATH $PATH:/usr/local/gcloud/google-cloud-sdk/bin


COPY my.json /
ENV GOOGLE_APPLICATION_CREDENTIALS my.json
