#### Things to check

1. check tmpdir2 folder have images or not, if no then

```shell
sudo mount -a
```

then check the folder content again. if the folder is still empty refer to Linux Mount below

2. check inside docker volume if there is any image in lane 1,2,3. refer step 2 in Docker
3. check if http post is error

```shell
docker logs anpr_netcore -f --tail 10
or
docker logs anpr_netcore_anpr_1 --since="10m"
```

check the log if there is error, if there is error http request, decompose everything and compose everything by following correct order

### Docker

Basic Docker command

```bash
docker ps -a (list currently running container)
docker images (list all images)
docker logs anpr_netcore_anpr_1 -f --tail 50 (logging by tail)
docker exec -it anpr_netcore_anpr_1 sh (container shell)
```

If images of ANPR are not loaded

1. Check container logs for error
2. Check if container volume is mirrored properly by navigating into container shell

```bash
docker exec -it anpr_netcore_anpr_1 sh
cd /app/anpr/fullimage/05-1/07-05-2023
ls
```

Ensure the .yml file is configured correctly to docker volume and local storage. If the images are not in the volume, restart the container. If local storage is empty, the mounting is problematic.

Refer to Linux Mount below to mount the drive. To restart the container, use this sequence and command.

```bash
# ignore WARNING and ERROR of orphan container and network as the container are orchestraed together

docker-compose -f offloader.dc.yml down
docker-compose -f netcore.docker-compose.yml down
docker-compose -f anpr.dc.yml down
docker-compose -f horizon.docker-compose.yml down

docker-compose -f horizon.docker-compose.yml up -d web
docker-compose -f anpr.dc.yml up -d
docker-compose -f netcore.docker-compose.yml up -d
docker-compose -f offloader.dc.yml up -d
```

3. Check docker logs again and see if the error persist.

### Linux Mount

Basic Linux command and tools

```bash
sudo (admin privilege)
cd (change directory)
mkdir (create directory)
touch (create new file)
nano (open text editor)
```

1. To mount the drive into the first pc. Check samba config in targeted drive.

```bash
nano /etc/samba/smb.conf

# Content should look like below

[Lane02_Images]
    path = /home/wim03-aipc02/anpr/tmpdir
    read only = no
    browsable = yes
    guest ok = yes

# to edit use sudo privilege
sudo nano /etc/samba/smb.conf
```

and make sure the fstab config is matched in 01 host of IPC (e.g. WIM02-AIPC01)

```bash
nano /etc/fstab

# Content should like like below
//10.32.64.33/Lane02_Images /home/wim02-aipc02/anpr/tmpdir cifs username=sdfvsdf-sdfvds,password=dcsadc,uid=1000,gid=1000,iocharset=utf8,_netdev,x-systemd.device-timeout=30,x-systemd.mount-timeout=10 0 0

# to edit use sudo privilege
sudo nano /etc/fstab
```

2. Ensure the mount is configured correctly and the directory is there, if directory is not there, create a new directory and use this command to mount all the drive stated in config to host

```bash
# if mount is not yet created
mkdir home/wim02-aipc02/anpr/tmpdir
sudo mount -a
```

3. Check the directory content to ensure the mount is connected to other host. Use this command to view if the drive is mounted

```bash
df -h

# Content should look like this
FileSystem                  Size   Used   Avail   Use%   Mounted on
//10.32.64.32/Lane02_Images 63M    21M    42M     33%    /home/wim02-aipc01/anpr/tmpdir2
```
