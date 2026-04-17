# Contenedores

### Crear un contenedor
Para crear un nuevo contenedor Docker a partir de una imagen específica, pero sin iniciarlo automáticamente. 

```
docker create --name <nombre contenedor> <nombre imagen>:<tag>
```
Crear el contenedor  **servidorr** usando la imagen nginx version alpine
```
PS C:\Users\Usuario> docker create --name servidorr nginx:alpine-perl
```
Si creas un contenedor en Docker sin asignarle un nombre específico utilizando la opción --name, Docker asignará automáticamente un nombre aleatorio al contenedor. Este nombre suele consistir en una combinación de palabras y números.  

Crear el contenedor usando la imagen hello-world
```
PS C:\Users\Usuario> docker create hello-world
```
### Listar los contenedores ejecutándose o no

```
docker ps -a
```

### Para iniciar un contenedor

```
docker start <nombre contenedor o identificador>
```
Iniciar el contenedor srv-web 
```
PS C:\Users\Usuario> docker start servidorr
```
### Listar los contenedores ejecutándose
```
docker ps 
docker ps | grep <nombre contenedor>
docker ps | grep servidorr
```

### Para detener un contenedor

```
docker stop <nombre contenedor>
docker stop servidorr
```

### Para crear un contenedor y ejecutarlo inmediatamente

```
docker run --name <nombre contenedor> <nombre imagen>:<tag>
PS C:\Users\Usuario> docker run --name helloo hello-world
```
![Ecosistema de Docker](dockerRun.PNG)

Crear y ejecutar inmediatamente el contenedor **srv-web2** usando la imagen nginx:alpine
**¿Qué sucede luego de la ejecución del comando?**
```
PS C:\Users\Usuario> docker run --name srv-web2 nginx:alpine-perl
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/04/17 04:05:13 [notice] 1#1: using the "epoll" event method
2026/04/17 04:05:13 [notice] 1#1: nginx/1.29.8
2026/04/17 04:05:13 [notice] 1#1: built by gcc 15.2.0 (Alpine 15.2.0)
2026/04/17 04:05:13 [notice] 1#1: OS: Linux 6.6.87.2-microsoft-standard-WSL2
2026/04/17 04:05:13 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2026/04/17 04:05:13 [notice] 1#1: start worker processes
2026/04/17 04:05:13 [notice] 1#1: start worker process 30
2026/04/17 04:05:13 [notice] 1#1: start worker process 31
2026/04/17 04:05:13 [notice] 1#1: start worker process 32
2026/04/17 04:05:13 [notice] 1#1: start worker process 33
2026/04/17 04:05:13 [notice] 1#1: start worker process 34
2026/04/17 04:05:13 [notice] 1#1: start worker process 35
2026/04/17 04:05:13 [notice] 1#1: start worker process 36
2026/04/17 04:05:13 [notice] 1#1: start worker process 37
2026/04/17 04:05:13 [notice] 1#1: start worker process 38
2026/04/17 04:05:13 [notice] 1#1: start worker process 39
2026/04/17 04:05:13 [notice] 1#1: start worker process 40
2026/04/17 04:05:13 [notice] 1#1: start worker process 41
2026/04/17 04:05:13 [notice] 1#1: start worker process 42
2026/04/17 04:05:13 [notice] 1#1: start worker process 43
2026/04/17 04:05:13 [notice] 1#1: start worker process 44
2026/04/17 04:05:13 [notice] 1#1: start worker process 45
2026/04/17 04:05:13 [notice] 1#1: start worker process 46
2026/04/17 04:05:13 [notice] 1#1: start worker process 47
2026/04/17 04:05:13 [notice] 1#1: start worker process 48
2026/04/17 04:05:13 [notice] 1#1: start worker process 49
```





Cuando ejecutas un contenedor en primer plano sin la opción -d (modo detach), el contenedor captura la entrada estándar (stdin) del terminal, lo que significa que el terminal queda "atrapado" y no puedes introducir más comandos hasta que detengas el contenedor.

### Para crear un contenedor y ejecutarlo inmediatamente sin estar vinculados al mismo
-d: Es la opción que indica a Docker que ejecute el contenedor en segundo plano (en modo "detach").
Cuando un contenedor se ejecuta en segundo plano, Docker devuelve el control al terminal inmediatamente después de iniciar el contenedor, lo que permite al usuario seguir ejecutando otros comandos en el mismo terminal sin que el contenedor detenga la interacción.

```
docker run -d --name <nombre contenedor> <nombre imagen>:tag
```
Crear y ejecutar inmediatamente el contenedor **srv-web3** en modo detach usando la imagen nginx:alpine
```
PS C:\Users\Usuario> docker run -d --name srv-web3 nginx:alpine-perl
b6c6c1945066999e4b943a9963ba9750de3afb13689472eb46f50989fb1ae314
```

### Para eliminar un contenedor

```
docker rm <nombre contenedor>


```
Eliminar el contenedor que se creó a partir de la imagen hello-world 
```
PS C:\Users\Usuario> docker rm epic_shannon
epic_shannon
```

Verificar que el contenedor que se eliminó
```
PS C:\Users\Usuario> docker ps
CONTAINER ID   IMAGE               COMMAND                  CREATED              STATUS              PORTS     NAMES
b6c6c1945066   nginx:alpine-perl   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    srv-web3
6091a9c653b8   nginx:alpine-perl   "/docker-entrypoint.…"   31 minutes ago       Up 22 minutes       80/tcp    servidorr
PS C:\Users\Usuario>

```

### Para eliminar un contenedor que esté ejecutándose

```
docker rm -f <nombre contenedor>
```
Eliminar el contenedor **srv-web3** 


```
docker rm -f srv-web3

```

Verificar que el contenedor que se eliminó

```
PS C:\Users\Usuario> docker rm -f srv-web3
srv-web3
PS C:\Users\Usuario> docker ps
CONTAINER ID   IMAGE               COMMAND                  CREATED          STATUS          PORTS     NAMES
6091a9c653b8   nginx:alpine-perl   "/docker-entrypoint.…"   34 minutes ago   Up 25 minutes   80/tcp    servidorr

```

### Para inspecionar un contenedor 

Inspeccionar el contenedor **servidorr** 
```
PS C:\Users\Usuario> docker inspect servidorr
[
    {
        "Id": "6091a9c653b8c2fe0893868508ef7055fb3dd86ea6931be73b0b070823c26d5a",
        "Created": "2026-04-17T03:39:48.993786115Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 529,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2026-04-17T03:48:43.60087049Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:0b8b38a871c9dbaebacf9da373e92196b625e3e19edea5084bc32bbd74f67f1c",
        "ResolvConfPath": "/var/lib/docker/containers/6091a9c653b8c2fe0893868508ef7055fb3dd86ea6931be73b0b070823c26d5a/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/6091a9c653b8c2fe0893868508ef7055fb3dd86ea6931be73b0b070823c26d5a/hostname",
        "HostsPath": "/var/lib/docker/containers/6091a9c653b8c2fe0893868508ef7055fb3dd86ea6931be73b0b070823c26d5a/hosts",
        "LogPath": "/var/lib/docker/containers/6091a9c653b8c2fe0893868508ef7055fb3dd86ea6931be73b0b070823c26d5a/6091a9c653b8c2fe0893868508ef7055fb3dd86ea6931be73b0b070823c26d5a-json.log",
        "Name": "/servidorr",
        "RestartCount": 0,
        "Driver": "overlayfs",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "bridge",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                90,
                113
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "private",
            "Dns": null,
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": null,
            "PidsLimit": null,
            "Ulimits": [],
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/acpi",
                "/proc/asound",
                "/proc/interrupts",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/sys/devices/virtual/powercap",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "Storage": {
            "RootFS": {
                "Snapshot": {
                    "Name": "overlayfs"
                }
            }
        },
        "Mounts": [],
        "Config": {
            "Hostname": "6091a9c653b8",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": true,
            "AttachStderr": true,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.29.8",
                "PKG_RELEASE=1",
                "DYNPKG_RELEASE=1",
                "NJS_VERSION=0.9.6",
                "NJS_RELEASE=1",
                "ACME_VERSION=0.3.1"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx:alpine-perl",
            "Volumes": null,
                    "MacAddress": "66:c1:82:3f:fd:18",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DNSNames": null
                }
            }
        },
        "ImageManifestDescriptor": {
            "mediaType": "application/vnd.oci.image.manifest.v1+json",
            "digest": "sha256:1aaf65f99c807ecf995740dd4bc6d09cf25f1f87fef657ad17d2a1e06999ecdc",
            "size": 2693,
            "annotations": {
                "com.docker.official-images.bashbrew.arch": "amd64",
                "org.opencontainers.image.base.digest": "sha256:c1263cc56873d66f381fd07149aa0dc7244dd7c941334cd18473c46509f08465",
                "org.opencontainers.image.base.name": "nginx:1.29.8-alpine",
                "org.opencontainers.image.created": "2026-04-07T18:03:05Z",
                "org.opencontainers.image.revision": "71081b25390771f6b1275ddf7c73c965f304493f",
                "org.opencontainers.image.source": "https://github.com/nginx/docker-nginx.git#71081b25390771f6b1275ddf7c73c965f304493f:mainline/alpine-perl",
                "org.opencontainers.image.url": "https://hub.docker.com/_/nginx",
                "org.opencontainers.image.version": "1.29.8-alpine-perl"
            },
            "platform": {
                "architecture": "amd64",
                "os": "linux"
            }
        }
    }
]
PS C:\Users\Usuario>

```
