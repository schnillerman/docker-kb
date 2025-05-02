All things docker

Here's a with self-reminders and shortcuts for docker management that I'm trying to optimize. Forking / optimization by others is very welcome.

# Helper Scripts
## Reset docker containers, networks, volumes
With _loop_:
```bash
for resource in container network volume; do
  docker "$resource" prune -f
done
```
With _xargs_:
```bash
echo "container network volume" | xargs -n1 sh -c 'docker "$0" prune -f'
```
# Security
## Docker Secrets
https://docs.docker.com/compose/how-tos/use-secrets/
#Shortcuts
## Variables
### .env
### Port Mappings
Can port mappings be conslidated and externalized by means of variables in order to keep track in case of a multitude of containers and mappings?
