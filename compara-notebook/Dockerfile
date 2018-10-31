FROM jupyter/scipy-notebook

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends ssh-client && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# install kubectl
RUN apt-get update && \
    apt-get install -y apt-transport-https curl gnupg && \
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >> /etc/apt/sources.list.d/kubernetes.list && \
    apt-get update && \
    apt-get install -y kubectl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# install docker
RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates curl software-properties-common  && \
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get install -y docker-ce && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# add user to docker group
RUN usermod -aG docker $NB_USER

# R pre-requisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    tzdata \
    gfortran \
    gcc && apt-get clean && \
    rm -rf /var/lib/apt/lists/*    

# add java8 oracle
RUN sudo add-apt-repository ppa:webupd8team/java && \
    echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | sudo debconf-set-selections && \
    sudo apt-get install -y oracle-java8-installer && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*



# Switch back to jovyan to avoid accidental container runs as root
USER $NB_UID
