FROM summerwind/actions-runner:v2.283.3-ubuntu-20.04

USER root

ARG TERRAFORM_VERSION=1.0.10
ARG TERRAFORM_SHA256="a221682fcc9cbd7fde22f305ead99b3ad49d8303f152e118edda086a2807716d"
RUN wget https://releases.hashicorp.com/terraform/$TERRAFORM_VERSION/terraform_"$TERRAFORM_VERSION"_linux_amd64.zip \
    && echo "$TERRAFORM_SHA256 terraform_"$TERRAFORM_VERSION"_linux_amd64.zip" | sha256sum -c \
    && unzip terraform_"$TERRAFORM_VERSION"_linux_amd64.zip \
    && rm terraform_"$TERRAFORM_VERSION"_linux_amd64.zip \
    && chmod +x terraform \
    && mv terraform /usr/local/bin/terraform \
    && terraform -version

ARG TERRAGRUNT_VERSION=0.35.5
ARG TERRAGRUNT_SHA256="fce3f667af7fdb3bba6acd1d73061ed10b2af36427c5056abdcb1c930a1a7ca4"
RUN wget https://github.com/gruntwork-io/terragrunt/releases/download/v"$TERRAGRUNT_VERSION"/terragrunt_linux_amd64 \
    && echo "$TERRAGRUNT_SHA256 terragrunt_linux_amd64" | sha256sum -c - \
    && chmod +x terragrunt_linux_amd64 \
    && mv terragrunt_linux_amd64 /usr/local/bin/terragrunt \
    && terragrunt --version

USER runner
