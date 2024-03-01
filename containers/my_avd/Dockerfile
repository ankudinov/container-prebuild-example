ARG FROM_IMAGE
ARG FROM_VARIANT

FROM ${FROM_IMAGE}:${FROM_VARIANT}

ARG USERNAME
ARG CLAB_VERSION
ARG AVD_GITHUB_REPO
ARG AVD_BRANCH_NAME

USER root

# install some basic tools inside the container
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    sshpass \
    iputils-ping \
    htop \
    && rm -rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && apt-get clean

USER ${USERNAME}

# install the latest containerlab, yamllint and eos-downloader
RUN bash -c "$(curl -sL https://get.containerlab.dev)" -- -v ${CLAB_VERSION} \
    && pip3 install --user yamllint \
    && pip install --user eos-downloader \
    && pip install --user passlib

# install Ansible collections
RUN pip3 install "$(curl -s https://raw.githubusercontent.com/${AVD_GITHUB_REPO}/${AVD_BRANCH_NAME}/ansible_collections/arista/avd/requirements-dev.txt | grep ansible-core)" \
    && ansible-galaxy collection install --force "git+https://github.com/${AVD_GITHUB_REPO}.git#/ansible_collections/arista/avd/,${AVD_BRANCH_NAME}" \
    && pip3 install -r ${HOME}/.ansible/collections/ansible_collections/arista/avd/requirements.txt -r ${HOME}/.ansible/collections/ansible_collections/arista/avd/requirements-dev.txt