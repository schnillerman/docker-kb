All things docker

Here's a with self-reminders and shortcuts for docker management that I'm trying to optimize. Forking / optimization by others is very welcome.

# Helper Scripts
## Reset docker containers, networks, volumes (but leave images)
With _loop_:
```bash
#!/bin/bash

# Stop and remove all containers (incl. running and volumes (-v))
docker ps -aq | xargs -r docker rm -vf

#Remove orphaned resources (volumes, networks, build cache) via loop
for resource in volume network system; do
  if [ "$resource" = "system" ]; then
    docker "$resource" prune -f  # System-Prune ohne --all (Keep images!)
  else
    docker "$resource" prune -f
  fi
done
```
or
```
#!/bin/bash

docker ps -aq | xargs -r docker rm -vf

# Only volume/network prune in Loop
for resource in volume network; do
  docker "$resource" prune -f
done

# separate system prune (Keep images)
docker system prune -f
```
With _xargs_:
```bash
#!/bin/bash

# Stop and remove all containers (incl. running and volumes (-v))
docker ps -aq | xargs -r docker rm -vf

# Remove orphaned volumes
docker volume prune -f

# Remove orphaned networks
docker network prune -f

# Delete build cache, keep images
docker system prune -f
```
## Total docker (container) reset
```bash
#!/bin/bash

# Stoppe und entferne alle Container (auch laufende) mit zugehörigen Volumes
docker ps -aq | xargs -r docker rm -vf

# Lösche alle unbenutzten Volumes (z. B. von früheren Containern)
docker volume prune -f

# Optional: Lösche ungenutzte Netzwerke, Images und Build-Cache
docker system prune -af --volumes
```
# Security
## Docker Secrets
https://docs.docker.com/compose/how-tos/use-secrets/
#Shortcuts
## Variables
### .env
### Port Mappings
Can port mappings be conslidated and externalized by means of variables in order to keep track in case of a multitude of containers and mappings?
