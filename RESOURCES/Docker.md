# What is Docker?
Docker is a packaging tool that helps to run an application by removing the dependency on OS, versions of the tech stack such as node JS, react Js, express JS and mongo DB etc, and  dependencies and other things by packaging it all together so we have the same environment for development that can be shared to make the application run uniformly.
Helps provide a common environment to run application in the form of "PACKAGED APPLICATION".

# What is Image and Container?
- Image
	- An image is a excutable package that helps run a piece of software which includes runtime, libraries, environment variables and configuration files.
	- It is a blueprint or template for creating a container.
	- Images are immutable and are stored in registries like docker hub.
- Container 
	- Runtime instance of a docker image. Its the actual execution of the image isolated from host system.
	- They are lightweight and portable running the software defined in the image.
Analogy :
Image is a recipe and the container is the cake made with t at recipe that can be eaten.

# Docker Volumes
Docker Volumes helps to make changes to our containers files via the local so they are reflected in the container instead of using docker exec which can achiece the same goal but is slightly more tedious.
Note: All changes made to container were not persisted to the host machine. So if we make a new container then changes lost.

docker run --mount type=bins,source=src-directory, target=dst-directory-in-container image-name
OR 
docker run -v host-path:dest-path image-name

# Dockerfile
Its a text document where each line is command to build our custom image.
Can be named anything but while building then ha to be passed as argument to be used to build the container.

# Commands
- docker images : Lists all the docker images on local.
- docker run image-name : Runs the docker image with name image-name and makes it a container.
- docker ps :Lists all images, by defualt its all the running containers
- docker rm image-name: Removes the given image. Needed as all images should have unique name. Can pass wither the name or the container id.
- docker run --name image-name -p 80:80 nginx : Runs the image and tell the local host to forward the request to the image thats running on that port. Here first 80 is the port of the host and the second 80 is the port of the container thats running.
- docker run --name image-name -p 80:80 -d nginx : does the same as above but in detached mode. This allows to run it separately so that in terminal if process is killed this nginx server is still up.
- docker logs image-name : Shows some logs
- docker logs -f image-name : Show constant logs like tail feature for linux.
- docker exec image-name : runs the command on the container.
- docker exec -it image-name bash: helps interact with the container in interactive mode and execute multiple commands.
- docker build -t image-name:version . : Builds the image you have added from the directrory. the '.' means the Dockerfile is in the current directory