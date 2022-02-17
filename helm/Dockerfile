ARG HELM_VERSION=3.8.0
FROM alpine:3.15 as download
ARG HELM_VERSION
WORKDIR /var/lib/helm
ADD https://get.helm.sh/helm-v${HELM_VERSION}-linux-amd64.tar.gz .
RUN apk add tar --no-cache --virtual .build-deps tar \
  && tar -xvf helm-v${HELM_VERSION}-linux-amd64.tar.gz \
  && apk del --no-network .build-deps

FROM alpine:3.15
WORKDIR /var/lib/helm
COPY --from=download /var/lib/helm/linux-amd64/helm . 
RUN ln -s /var/lib/helm/helm /bin/helm