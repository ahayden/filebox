# Run an SMB file server as a container 
This is a stateful approach but does not use config files migrated from a prior 
install on the docker host.

Dockerfile and compose elements taken from 
[alubbock/samba-docker](https://github.com/alubbock/samba-docker)

### Bootstrap
- `docker exec -it $containerid /bin/bash`
- `useradd $username`
- `useradd $username sambashare`
- `smbpasswd -a $username`
- `chown root:sambashare /mnt/share`
- `chmod -R 0770 /mnt/share`

