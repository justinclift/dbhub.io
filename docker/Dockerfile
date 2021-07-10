# vim:set ft=dockerfile:
FROM alpine:3.14

LABEL maintainer="Justin Clift <justin@postgresql.org>"

# Install Git, Go, and SQLite-dev
RUN  \
    apk update && \
    apk upgrade && \
    apk add --no-cache ca-certificates 'curl>7.61.0' git go libc-dev sqlite-dev

# Create the DBHub.io OS user
RUN addgroup dbhub && \
    adduser -D -S -s /bin/ash -G dbhub dbhub

# Set the dependencies and DBHub.io daemons to automatically start
ENTRYPOINT /usr/local/bin/start.sh

# Create directores for the DBHub daemons
RUN mkdir -p /var/log/dbhub ~dbhub/.dbhub/disk_cache ~dbhub/.dbhub/email_queue && \
    chown -R dbhub:dbhub /var/log/dbhub ~dbhub/.dbhub/disk_cache ~dbhub/.dbhub/email_queue && \
    chmod 700 /var/log/dbhub ~dbhub/.dbhub/disk_cache ~dbhub/.dbhub/email_queue

# Config file
ENV CONFIG_FILE /go/src/github.com/sqlitebrowser/dbhub.io/docker/config.toml

# Add script pieces for starting DBHub.io services
RUN echo "echo 127.0.0.1 docker-dev.dbhub.io docker-dev >> /etc/hosts" >> /usr/local/bin/start.sh && \
    echo "su - dbhub -c 'CONFIG_FILE=${CONFIG_FILE} /usr/local/bin/dbhub-webui &'" >> /usr/local/bin/start.sh && \
    echo "su - dbhub -c 'CONFIG_FILE=${CONFIG_FILE} /usr/local/bin/dbhub-db4s &'" >> /usr/local/bin/start.sh && \
    echo "su - dbhub -c 'CONFIG_FILE=${CONFIG_FILE} /usr/local/bin/dbhub-api'" >> /usr/local/bin/start.sh && \
    chmod +x /usr/local/bin/start.sh

# Include the source code to be compiled
COPY . /go/src/github.com/sqlitebrowser/dbhub.io

# Build the DBHub.io daemons
RUN cd /go/src/github.com/sqlitebrowser/dbhub.io &&  \
    go build -gcflags "all=-N -l" -o /usr/local/bin/dbhub-api github.com/sqlitebrowser/dbhub.io/api && \
    go build -gcflags "all=-N -l" -o /usr/local/bin/dbhub-db4s github.com/sqlitebrowser/dbhub.io/db4s && \
    go build -gcflags "all=-N -l" -o /usr/local/bin/dbhub-webui github.com/sqlitebrowser/dbhub.io/webui
