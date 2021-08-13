# Run SMB file server as a container 
This is a stateful approach but does not use config files migrated from a prior 
install on the docker host.

Dockerfile and compose elements taken from 
[alubbock/samba-docker](https://github.com/alubbock/samba-docker)

### Bootstrap
- On docker host: add storage, ie:
  - `parted /dev/nvme0n1 mklabel gpt`
  - `parted -a optimal /dev/nvme0n1 mkpart primary 0% 100%`
  - Append UUID to fstab
  - `groupadd --gid 511`
  - `chown root:sambashare /mnt/storage`
  - `chmod -R 0770 /mnt/storage`
- In container: `docker exec -it $containerid /bin/bash`
  - `useradd $username`
  - `adduser $username sambashare`
  - `smbpasswd -a $username`

Note: the GID value of `sambashare` is defined in [Dockerfile.base](Dockerfile.base)
and should by synchronized with a GID on the docker host, or at least not conflict.

