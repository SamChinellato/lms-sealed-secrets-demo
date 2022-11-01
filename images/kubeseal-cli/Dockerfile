FROM registry.access.redhat.com/ubi8:latest

ENV KUBESEAL_VERSION=0.19.1

RUN curl -sL https://github.com/bitnami-labs/sealed-secrets/releases/download/v${KUBESEAL_VERSION}/kubeseal-${KUBESEAL_VERSION}-linux-amd64.tar.gz \
    --output kubeseal-${KUBESEAL_VERSION}-linux-amd64.tar.gz

RUN tar -xvzf kubeseal-${KUBESEAL_VERSION}-linux-amd64.tar.gz kubeseal && \
    install -m 755 kubeseal /usr/local/bin/kubeseal && \
    kubeseal --version

CMD ["/usr/local/bin/kubeseal"]