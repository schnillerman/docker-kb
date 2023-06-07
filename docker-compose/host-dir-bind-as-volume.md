In order to define a block with volumes and still use host directories instead of docker volumes, volumes can be defined as follows:
```
volumes:
  <volume-id/-name>:
    driver_opts:
      device: <host directory path>
      o: bind
      type: local
```
