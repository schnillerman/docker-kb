A script that uses the directory name of the docker-compose.yml as container_name prefix.
```
export CURRENTDIR=${PWD##*/} && echo "creating container with $CURRENTDIR as prefix ..." && docker-compose up -d
```
I recommend to save as an `sh` script in the root direcctory of your container storage. If you change to the `docker-compose.yml` directory, just call `../<script name>.sh` and you're good to go.
