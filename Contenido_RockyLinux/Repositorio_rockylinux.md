# ¿Dónde se encuentran los repositorios?
Para poder instalar los repositorios de Rocky linux debemos escribir este comando:
- wget -P $repos_base_dir https://dl.rockylinux.org/pub/rocky/RPM-GPG-KEY-rockyofficial

Tambien, si lo que queremos es agregar los repositorios a un servidor web, podemos usar este script que se encuentra en
la pagina oficial de Rocky linux para subirlo:
#!/bin/bash
repos_base_dir="/web/path"

# Start sync if base repo directory exist
if [[ -d "$repos_base_dir" ]] ; then
  # Start Sync
  rsync  -avSHP --progress --delete --exclude-from=/opt/scripts/excludes.txt rsync://ord.mirror.rackspace.com/rocky  "$repos_base_dir" --delete-excluded
  # Download Rocky 8 repository key
  if [[ -e /web/path/RPM-GPG-KEY-rockyofficial ]]; then
     exit
  else
      wget -P $repos_base_dir https://dl.rockylinux.org/pub/rocky/RPM-GPG-KEY-rockyofficial
  fi
fi
