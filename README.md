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
