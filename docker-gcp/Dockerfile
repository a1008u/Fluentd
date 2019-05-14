FROM fluentd:latest

USER root
RUN apk update && apk add python \
    python-dev  \
    tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    apk del tzdata && \
    rm -rf /var/cache/apk/*

ENV PYTHON_PIP_VERSION 19.1.1

RUN set -ex; \
	\
	wget -O get-pip.py 'https://bootstrap.pypa.io/get-pip.py'; \
	\
	python get-pip.py \
		--disable-pip-version-check \
		--no-cache-dir \
		"pip==$PYTHON_PIP_VERSION" \
	; \
	pip --version; \
	\
	find /usr/local -depth \
		\( \
			\( -type d -a \( -name test -o -name tests \) \) \
			-o \
			\( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
		\) -exec rm -rf '{}' +; \
rm -f get-pip.py

RUN apk add sudo \
 curl \
 vim \
 git

# Fluentd GCSプラグインインストール
RUN gem install fluent-plugin-gcs -v "0.4.0"

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