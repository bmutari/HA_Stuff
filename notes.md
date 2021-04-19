DOCKER
*** under docker-compose ***
To update HA: 
sudo docker pull homeassistant/home-assistant:stable (new new image from docker hub)
sudo docker-compose stop homeassistant (stop the current HA container, needs to be run from the dir with the docker-compose file in it)
sudo docker-compose up -d --force-recreate homeassistant (restart HA container using the new image; -d for detach in term)



Home Assistant run cmd:
sudo docker run --init -d --name="ha" -v /home/brandon/docker_data/homeassistant:/config --net=host --device=/dev/ttyACM0 --restart=unless-stopped homeassistant/home-assistant

--init : Run an init inside the container that forwards signals and reaps processes
-d : detach 
--name : name for the container
-v : volume to bind mount (also where all HA settings and db's are stored)
--net : use the host (Ubuntu) network i.e. container will have ip of host machine all ports
--device : pass into the container the zwave usb stick ( /dev/ttyACM0 )
--restart : unless-stopped= restart the container after an exit 
-e TZ=America/Denver - sets an env var in the container for timezone, needed for NodeRED to set timers in local time. 

Node RED
docker run -d -p 1880:1880 -v /home/brandon/docker_data/:/data --name nr --restart=unless-stopped -e TZ=America/Denver nodered/node-red

Cleaning up docker::::::

Purging All Unused or Dangling Images, Containers, Volumes, and Networks
Docker provides a single command that will clean up any resources — images, containers, volumes, and networks — that are dangling (not associated with a container):

docker system prune

To additionally remove any stopped containers and all unused images (not just dangling images), add the -a flag to the command:

docker system prune -a
Removing Docker Images
Remove one or more specific images
Use the docker images command with the -a flag to locate the ID of the images you want to remove. This will show you every image, including intermediate image layers. When you’ve located the images you want to delete, you can pass their ID or tag to docker rmi:

List:

docker images -a
Remove:

docker rmi Image Image

Postgres: 
Two containers 1. postgres 2. pgadmin 
User for postgres is "postgres" password in the docker-compose.yml file
pgadmin running on port 5050 and mapped to port 80 of the container
