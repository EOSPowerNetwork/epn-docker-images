# Intro
This code is used to build a docker image that configures an ubuntu environment with the tools necessary to build eos smart contracts compiled with the clsdk (rather than the cdt by B1). Additionally, the version of EOS installed on the machine is 2.0.13 + a special plugin to service pull transactions via the EOS Power Network.

## How to use
No one really needs to use this repo. Just use the docker image (will be linked above when available) if you want a development environment preconfigured for eos with the EPN plugin and the clsdk.

# Command used to build the docker image
```docker image build -t jamesmart/eos-epn-clsdk:latest .```