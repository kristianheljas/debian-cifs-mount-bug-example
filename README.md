# Demonstration of Docker cifs mount error on debian

Reproduction steps:

```shell
vagrant up
vagrant ssh

# Inside vagrant machine    
sudo docker volume create --driver local --opt type=cifs --opt device=//127.0.0.1/media --opt o=guest,uid=vagrant,gid=vagrant media
sudo docker run --rm -it -v media:/mnt/media ubuntu bash
```

When attempting to run container with this mount, following error is produced:

```
docker: Error response from daemon: error while mounting volume '/var/lib/docker/volumes/media/_data': failed to mount local volume: mount //127.0.0.1/media:/var/lib/docker/volumes/media/_data, data: guest,uid=vagrant,gid=vagrant: invalid argument.
```
