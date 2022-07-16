# docker-new-eos-contract_multi-class

The github repo for the docker hub container: jamesmart/new-multi-class-eos-contract:latest

## Sample image build for this image

```docker image build -t jamesmart/new-multi-class-eos-contract:latest .```

### Sample container run for this image

```docker container run -it -v MyVolume1:/root/ --name MyEOSContainer1 jamesmart/new-multi-class-eos-contract:latest bash -c "cd /root/EOS; bash"```
