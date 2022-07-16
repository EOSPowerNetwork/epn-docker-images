FROM jamesmart/eosio-clsdk:latest

# Pass the project name (Which is the project root directory) into the container as an environment variable
ENV PROJ="eos"

# Install dependencies
RUN apt-get update \
    && apt-get install -yq   \
        unzip                \
        clang-tidy           \
        clang-format

# Download the EOS smart contract template repo
ADD https://github.com/EOSPowerNetwork/eos-contract-template/archive/refs/heads/main.zip /root/

# Decompress
WORKDIR /root
RUN unzip main.zip    \
    && rm main.zip    \
    && mv eos-contract-template-main/ ${PROJ}/

# Build
WORKDIR /root/${PROJ}
RUN mkdir build
WORKDIR /root/${PROJ}/build
RUN cmake `clsdk-cmake-args` ..
RUN make -j $(nproc)

# Switch back into source directory
WORKDIR /root/${PROJ}/
