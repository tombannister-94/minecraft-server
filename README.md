Minecraft Server - tombannister-94
===================

Setup
-----

To get started you need Docker ([Windows](https://docs.docker.com/docker-for-windows/install/), [OSX](https://docs.docker.com/docker-for-mac/install/), [Linux](https://docs.docker.com/install/linux/docker-ce/centos/)) and [Docker Compose](https://docs.docker.com/compose/install/) installed.

Inside of the `docker-compose.yml` file is a `volume` setting which contains the path to where the Minecraft server data will store to. You'll want to update that path to wherever you want your data to be stored, but remember to keep `:/data` at the end of your path.


Running the server
-------------------

Bring up the server with docker compose:

    $ docker-compose up

Or to bring up a specific server, for example the `mc_survival` server:

    $ docker-compose up mc_survival

Head into Minecraft and connect to the server with `localhost:{port_number}`.

Server data is stored into `{volume_path}/{server_name}/`.

It's that simple.


Changing an existing servers settings
-------------------

To change server settings but keep the Minecraft world data, you can do so by editing your `docker-compose.yml` environment with a bunch of different settings discussed [here](https://github.com/itzg/docker-minecraft-server/blob/master/README.md).

Once updated you'll want to stop your server, head to your `{volume_path}/{server_name}` and delete `server.properties`. Re-run your server and a new `server.properties` file will be created with your new settings. You could be lazy and edit `server.properties` directly, but that's on you if you lose the world data and can't remember any custom settings you set.


Further setup
-------------------

If you wish to customize settings further, the Docker image can be found [here](https://hub.docker.com/r/itzg/minecraft-server), while its docs are [here](https://github.com/itzg/docker-minecraft-server/blob/master/README.md).

Multiple servers can be run by creating another service in the `docker-compose.yml` file. The port will need to be unique, but remember the default Minecraft port is `25565` so this will need to remain the same. A basic example might be:

```
 mc_second_server:
    image: itzg/minecraft-server
    ports:
      - "25570:25565"
    volumes:
      - "/home/tom/code/minecraft-server/data/mc_second_server:/data"
    environment:
      EULA: "TRUE"
      MOTD: "A second server hosted by tombannister-94"
```

Connect to it in Minecraft via `localhost:25570`. 


World data
-------------------

The servers data is stored inside the `{volume_path}/{server_name}` directory and is ignored by Git. For serious servers, I'd recommend backing up this directory often. As long as the volume in your `docker-compose.yml` matches the path to the data directory, you can spin up the server wherever you're hosting from and all of your data will be there.
