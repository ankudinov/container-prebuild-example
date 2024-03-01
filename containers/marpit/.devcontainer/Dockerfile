ARG FROM_IMAGE
ARG FROM_VARIANT

FROM ${FROM_IMAGE}:${FROM_VARIANT}

ARG USERNAME

USER ${USERNAME}
RUN sudo apt-get update \
    && sudo apt-get install -y chromium