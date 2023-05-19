# How to run MySql through Docker


To run mysql through docker run the following
```
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD="my-secret-pw" -p 3306:3306 -d mysql:tag
```

Example to run mysql on version 8
```
docker run --name local-mysql8 -e MYSQL_ROOT_PASSWORD="my-secret-pw" -p 3306:3306 -d mysql:8
```

MacOS M+ CPU:
Add `--platform linux/x86_64` parameter

Reference: https://hub.docker.com/_/mysql
