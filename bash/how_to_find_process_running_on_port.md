# How to find process running on port

```
netstat -tulpn
```

This will print the tcp adresses and ports and also the process id. With the process ID its possible to kill the process by using

```
kill {PID}
```