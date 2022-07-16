# docker-new-eos-contract

The github repo for the docker hub container: jamesmart/new-eos-contract:latest

## Sample image build for this image

```docker image build -t jamesmart/new-eos-contract:latest .```

### Sample container run for this image

```docker container run -it -v MyVolume1:/root/ --name MyEOSContainer1 jamesmart/new-eos-contract:latest bash -c "cd /root/EOS; bash"```
