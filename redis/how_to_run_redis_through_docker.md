## How to run redis through docker

Its possible to run redis on any machine using docker containers. So its possible to start the redis container image and then start bash, and then start redis cli.

```
docker run --name my-redis -d redis redis-server --appendonly yes
docker container run -p 6379:6379 redis -d
docker container exec -it my-redis "/bin/bash"
redis-cli
127.0.0.1:6379> set farhad likes:stackoverflow
OK
127.0.0.1:6379> get farhad
"likes:stackoverflow"
```