Forked from https://github.com/othrayte/docker-cc-amp

# AMP Dockerfile
Dockerfile for a container that installs and starts a Application Management Panel module from CubeCoders.com

Installs the Application Management Panel from CubeCoders.
 
This container requires a valid AMP license to run

## Changes since fork
- added sqlite3
- switched from Java 7 to Java 9


## Running minecraft (with an AMP licence)

### Using environment vars

The defaults are 

```
MODULE=Minecraft
EXTRAS="+MinecraftModule.Minecraft.PortNumber 25565"
```

Create an enviroment variable file (called something like "amp-env.list") with the following contents

```
LICENCE=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

Running the container is then as simple as:

`docker run -p 8080:8080 -p 25565:25565 --env-file ./amp-env.list anansii/amp-minecraft`


Or add some options:
```
LICENCE=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
EXTRAS=+MinecraftModule.Minecraft.PortNumber 30000
PORT=9000 
```
In this case EXTRAS overwrites the default port to 30000 for Minecraft and PORT to 9000 for AMP 


Running the container is then as simple as:

`docker run -p 9000:9000 -p 25565:25565 --env-file ./amp-env.list anansii/amp-minecraft`

### Directly passing options

Another method is to pass the required options directly to the container.

With defaults

`docker run -p 8080:8080 -p 25565:25565 anansii/amp-minecraft --licence-key your-licence-key-xxxx`

With port change:

`docker run -p 8080:8080 -p 25565:25565 anansii/amp-minecraft --licence-key your-licence-key-xxxx +MinecraftModule.Minecraft.PortNumber 30000`


Both of these methods create a docker container with the Minecraft module for AMP. You can login to the administrative console at port (default) 8080 with the username "admin" and password "password"; change the password when you first login. From here it is a standard AMP Minecraft module.


## Options

Most arguments to the container, and to the AMP modules inside it, can be passed as either command line arguments or enviroment variables.

| Argument | Env var | Default | Description |
| -------- | ------- | ------- | ----------- |
| 1st argument | | `MODULE` | No default | The AMP module to make an instance of |
| `-l`, `--licence-key` | `LICENCE` | No default | Your AMP licence key |
| `-n`, `--instance-name` | `INSTANCE_NAME` | "Instance" | The name to call the instance |
| `-p`, `--password` | `PASSWORD` | "password" | Initial password for the admin amp instance user |
| `-u`, `--username` | `USERNAME` | "admin" | Initial username for the admin amp instance user |
| `-h`, `--host` | `HOST` | "0.0.0.0" | The network interface to listen on, "0.0.0.0" is all interfaces |
| `--port` | `PORT` | "8080" | The network port to listen on |
| `+OOOOO` | `EXTRAS` | No default | Extra options that are passed to the AMP module |

Note: Extra options should each be in the format `+MyOption Value`, when specified in the enviroment variable multiple options can be added separated by spaces