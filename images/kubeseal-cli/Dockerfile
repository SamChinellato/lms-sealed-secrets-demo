FROM registry.access.redhat.com/ubi8:latest

ENV KUBESEAL_VERSION=0.16.0

RUN curl -L https://github.com/bitnami-labs/sealed-secrets/releases/download/v${KUBESEAL_VERSION}/kubeseal-linux-amd64 \
    --output kubeseal

RUN install -m 755 kubeseal /usr/local/bin/kubeseal && \
    kubeseal --version

CMD ["/usr/local/bin/kubeseal"]