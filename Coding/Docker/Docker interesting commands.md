```bash
docker ps --filter name=tcore* --filter status=running -aq | xargs docker stop
```

this will stop/kill/remove/start/restart any container that coincides with that input


Stop all the containers

```bash
docker stop $(docker ps -a -q)
```

Remove all the containers

```bash
docker rm $(docker ps -a -q)
```



