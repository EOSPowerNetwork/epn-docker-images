FROM ubuntu:focal

# Install dependencies
RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -yq      \
        binaryen                \
        build-essential         \
        cmake                   \
        curl                    \
        gdb                     \
        git                     \
        libboost-all-dev        \
        libcurl4-openssl-dev    \
        libgmp-dev              \
        libssl-dev              \
        libtinfo5               \
        libusb-1.0-0-dev        \
        libzstd-dev             \
        llvm-11-dev             \
        ninja-build             \
        pkg-config              \
        time                    \
        wget                    \
    && apt-get clean -yq \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /root

# Install EOS
RUN git clone -b epn-plugin --single-branch https://github.com/EOSPowerNetwork/eos.git
WORKDIR /root/eos
RUN git submodule update --init --recursive

# Generate EOS makefile
RUN mkdir build
WORKDIR /root/eos/build
RUN cmake -DCMAKE_BUILD_TYPE=Release -DDISABLE_WASM_SPEC_TESTS=yes ..

# Build EOS
RUN make -j $(nproc)

# Install EOS
RUN make install

# Clean up repository
WORKDIR /root
RUN rm -rf eos

# Install the wasi sdk
WORKDIR /opt
RUN curl -fLO https://github.com/WebAssembly/wasi-sdk/releases/download/wasi-sdk-12/wasi-sdk-12.0-linux.tar.gz \
    && tar xf wasi-sdk-12.0-linux.tar.gz \
    && rm wasi-sdk-12.0-linux.tar.gz
ENV WASI_SDK_PREFIX=/opt/wasi-sdk-12.0

# Install clsdk 
RUN curl -fLO https://github.com/eoscommunity/Eden/releases/download/sdk-v0.2.0-alpha/clsdk-ubuntu-20-04.tar.gz \
    && tar xf clsdk-ubuntu-20-04.tar.gz \
    && rm clsdk-ubuntu-20-04.tar.gz
ENV PATH=$PATH:/opt/clsdk/bin

# Set up optional development UX improvements
## Bash shell is needed to use ansi-c quotes
SHELL ["/bin/bash", "-c"]

RUN echo $'\n\
parse_git_branch() {\n\
  git branch 2> /dev/null | sed -e "/^[^*]/d" -e "s/* \\(.*\\)/ (\\1)/"\n\
} \n\
export PS1="\u@\h \W\[\\033[32m\\]\\$(parse_git_branch)\\[\\033[00m\\] $ "\n\
if [ -f ~/.git-completion.bash ]; then\n\
  . ~/.git-completion.bash\n\
fi\n\
' >> /root/.bashrc
