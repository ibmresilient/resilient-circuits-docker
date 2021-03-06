# Base image with required OS packages
FROM python:3.7-alpine

# required packages add in alphabetical order for easier reading
RUN apk update && \
  apk add --no-cache --virtual .build-deps \
    abuild \
    bash \
    binutils \
    build-base \
    gcc \
    git \
    libffi \
    libffi-dev \
    openssl \
    openssl-dev

# Get latest pip and install circuits
RUN pip install --upgrade pip && \
  pip install resilient>=34.0.195 \
    resilient-circuits>=34.0.195 \
    resilient-lib>=34.0.195

# Set up configuraiton and log locations using /etc and /var/log, the conventional locations for config and logs
RUN mkdir /etc/circuits
ENV APP_CONFIG_FILE /etc/circuits/app.config

RUN mkdir /var/log/circuits
ENV APP_LOG_DIR /var/log/circuits

# Entrypoint for circuits.  Use /opt, the conventional location for optional software on Linux
RUN mkdir /opt/circuits
COPY /assets/entrypoint.sh /opt/circuits/entrypoint.sh
ENTRYPOINT [ "sh", "/opt/circuits/entrypoint.sh" ]
