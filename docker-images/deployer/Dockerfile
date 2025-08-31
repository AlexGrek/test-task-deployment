FROM alpine:3.19

ARG KUBECTL_VERSION=v1.33.4
ARG HELM_VERSION=v3.18.4

ENV KUBECTL_VERSION=${KUBECTL_VERSION}
ENV HELM_VERSION=${HELM_VERSION}

ENV SHELL=/bin/bash

RUN apk add --no-cache \
    curl \
    git \
    make \
    bash \
    ca-certificates \
    openssh-client

# Install kubectl
RUN curl -LO "https://dl.k8s.io/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl" && \
    chmod +x kubectl && \
    mv kubectl /usr/local/bin/


RUN curl -LO "https://get.helm.sh/helm-${HELM_VERSION}-linux-amd64.tar.gz" && \
    tar -zxvf helm-${HELM_VERSION}-linux-amd64.tar.gz && \
    mv linux-amd64/helm /usr/local/bin/helm && \
    rm -rf helm-${HELM_VERSION}-linux-amd64.tar.gz linux-amd64

RUN mkdir -p /root/.kube

RUN kubectl version --client && \
    helm version && \
    git --version && \
    make --version

WORKDIR /workspace

CMD ["/bin/bash"]
