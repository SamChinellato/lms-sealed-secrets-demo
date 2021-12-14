FROM registry.access.redhat.com/ubi8:latest

ENV KUBECTL_VERSION=1.23.0

RUN curl -LO https://dl.k8s.io/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl

RUN install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
    kubectl version --client=true

CMD ["/usr/local/bin/kubectl"]