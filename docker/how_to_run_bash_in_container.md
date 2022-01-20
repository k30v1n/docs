# How to run bash in docker container

Offen we need to start the docker container and run the bash CLI on it to check and query the image that is being built. The steps bellow translate how to do that.

```
docker build -t image . --no-cache
docker container run -e ENV_VAR="value" --rm -p 3001:80 --name container_name image_name:latest
docker container exec -it [container] "/bin/bash"
```