# AUTOGENERATED FILE
FROM balenalib/i386-nlp-debian:sid-run

ENV GO_VERSION 1.10.8

# gcc for cgo
RUN apt-get update && apt-get install -y --no-install-recommends \
		g++ \
		gcc \
		libc6-dev \
		make \
		pkg-config \
		git \
	&& rm -rf /var/lib/apt/lists/*

RUN set -x \
	&& fetchDeps=' \
		curl \
	' \
	&& apt-get update && apt-get install -y $fetchDeps --no-install-recommends && rm -rf /var/lib/apt/lists/* \
	&& mkdir -p /usr/local/go \
	&& curl -SLO "http://resin-packages.s3.amazonaws.com/golang/v$GO_VERSION/go$GO_VERSION.linux-i386.tar.gz" \
	&& echo "4fd03c176c0f44d0e397fde4964306f36e17ae5e28141789618553144d476dd6  go$GO_VERSION.linux-i386.tar.gz" | sha256sum -c - \
	&& tar -xzf "go$GO_VERSION.linux-i386.tar.gz" -C /usr/local/go --strip-components=1 \
	&& rm -f go$GO_VERSION.linux-i386.tar.gz

ENV GOROOT /usr/local/go
ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

CMD ["echo","'No CMD command was set in Dockerfile! Details about CMD command could be found in Dockerfile Guide section in our Docs. Here's the link: https://balena.io/docs"]

 RUN curl -SLO "https://raw.githubusercontent.com/balena-io-library/base-images/8accad6af708fca7271c5c65f18a86782e19f877/scripts/assets/tests/test-stack@golang.sh" \
  && echo "Running test-stack@golang" \
  && chmod +x test-stack@golang.sh \
  && bash test-stack@golang.sh \
  && rm -rf test-stack@golang.sh 

RUN [ ! -d /.balena/messages ] && mkdir -p /.balena/messages; echo 'Here are a few details about this Docker image (For more information please visit https://www.balena.io/docs/reference/base-images/base-images/): \nArchitecture: Intel 32-bit (x86) for Intel Quark \nOS: Debian Sid \nVariant: run variant \nDefault variable(s): UDEV=off \nThe following software stack is preinstalled: \nGo v1.10.8 \nExtra features: \n- Easy way to install packages with `install_packages <package-name>` command \n- Run anywhere with cross-build feature  (for ARM only) \n- Keep the container idling with `balena-idle` command \n- Show base image details with `balena-info` command' > /.balena/messages/image-info

RUN echo '#!/bin/sh.real\nbalena-info\nrm -f /bin/sh\ncp /bin/sh.real /bin/sh\n/bin/sh "$@"' > /bin/sh-shim \
	&& chmod +x /bin/sh-shim \
	&& cp /bin/sh /bin/sh.real \
	&& mv /bin/sh-shim /bin/sh