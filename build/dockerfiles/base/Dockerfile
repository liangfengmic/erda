FROM --platform=$TARGETPLATFORM golang:1.19-bullseye

# set timezone to CST
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# libgit2-1.3
RUN echo "deb http://deb.debian.org/debian bookworm main" >> /etc/apt/sources.list
RUN apt update && apt install -y --no-install-recommends --no-install-suggests \
    cmake \
    gcc \
    g++ \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    libssl-dev \
    vim \
    jq \
    python3-pip \
    # for libgit2
    libgit2-1.3 libgit2-dev \
 && rm -fr /var/lib/apt/lists/*

# nodejs
RUN curl -sL https://deb.nodesource.com/setup_lts.x | bash - && apt install -y nodejs npm && rm -fr /var/lib/apt/lists/*

# docker-cli
RUN mkdir -p /etc/apt/keyrings \
 && curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg \
 && echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null \
 && apt update && apt install -y --no-install-recommends --no-install-suggests \
    docker-ce-cli \
 && rm -fr /var/lib/apt/lists/*

# librdkafka
# doc: https://github.com/confluentinc/confluent-kafka-go#librdkafka
# summary: Prebuilt librdkafka binaries are included with the Go client and librdkafka does not need to be installed separately on the build or target system.
# see: /go/pkg/mod/github.com/confluentinc/confluent-kafka-go@v1.5.2/kafka/librdkafka

# libgit2 - normal installation if specific version cannot install through APT.
## doc: https://github.com/libgit2/git2go#installing
## summary: This project wraps the functionality provided by libgit2. If you're using a versioned branch, install it to your system via your system's package manager and then install git2go.
#RUN cd "$HOME" && \
#    git clone https://github.com/libgit2/libgit2.git -b v1.3.1 --depth 1 && \
#    cd libgit2 && \
#    rm -rf build && mkdir build && cd build && \
#    cmake .. -DBUILD_CLAR=OFF && cmake --build . --target install
