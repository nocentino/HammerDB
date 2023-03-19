FROM ubuntu:20.04

# For apt install without question
ARG DEBIAN_FRONTEND=noninteractive

# Set working directory
WORKDIR /home/hammerdb

#Install packages, configure shell and clean up cache
RUN apt-get update && \
    apt-get install -y apt-transport-https curl gnupg2 wget python3 vim && \
    curl -sSL https://packages.microsoft.com/config/ubuntu/20.04/prod.list | tee /etc/apt/sources.list.d/microsoft-prod.list && \
    curl -sSL https://packages.microsoft.com/keys/microsoft.asc | tee /etc/apt/trusted.gpg.d/microsoft.asc && \
    apt-get update && ACCEPT_EULA=Y apt-get install -y mssql-tools18 msodbcsql18 unixodbc unixodbc-dev && \
    echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.bashrc && \
    /bin/bash -c "source ~/.bashrc" && \
    apt-get clean && \
    rm -rf /var/apt/cache/* /tmp/* /var/tmp/* /var/lib/apt/lists

# Install configure HammerDB-v4.7...change this to get the latest
RUN wget https://github.com/TPC-Council/HammerDB/releases/download/v4.7/HammerDB-4.7-Linux.tar.gz && \
    tar -xvzf HammerDB-4.7-Linux.tar.gz && ls && \
    echo 'export LD_LIBRARY_PATH=/usr/lib/x86_64-linux-gnu/:$LD_LIBRARY_PATH'  >> ~/.bashrc

WORKDIR /home/hammerdb/HammerDB-4.7

# Adding some sample scripts to be used with HammerDB command line interface
ADD scripts /home/hammerdb/HammerDB-4.7/scripts

CMD "bash"