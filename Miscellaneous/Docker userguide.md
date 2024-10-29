Tutorial from https://www.docker.com/101-tutorial/

1. Open Docker Desktop. (Download [here](https://www.docker.com/products/docker-desktop) if you don’t have it).
2. Type the following command in your terminal: `docker run -dp 80:80 docker/getting-started`
3. Open your browser to [http://localhost](http://localhost)
4. Have fun!

---

## Run a container

First step, run the following container to start :

```
docker run -d -p 80:80 docker/getting-started
```

You'll notice a few flags being used. Here's some more info on them:

- `-d` - run the container in detached mode (in the background)
- `-p 80:80` - map port 80 of the host to port 80 in the container
- `docker/getting-started` - the image to use
  Go to [http://localhost](http://localhost) to open the product.

## Build a container

```
docker build -t getting-started .
```

- `docker build` - build a new container image
- `-t getting-started` - tag the image
- `.` - tells that Docker should look for the `Dockerfile` in the current directory

## Create named volume

```
docker volume create todo-db
```

## Run a container with a volume

```
docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started
```

- `-v` - flag to specify a volume to mount
- `todo-db:/etc/todos` - name of volume to use, and path to mount the volume
- `docker/getting-started` - the image to use

## Get the volume location
```
docker volume inspect todo-db
```

## Starting a dev-mode container
```
docker run -dp 3000:3000 \
    -w /app -v "$(pwd):/app" \
    node:18-alpine \
    sh -c "yarn install && yarn run dev"
```
- `-dp 3000:3000` - same as before. Run in detached (background) mode and create a port mapping
- `-w /app` - sets the container's present working directory where the command will run from
- `-v "$(pwd):/app"` - bind mount (link) the host's present `getting-started/app` directory to the container's `/app` directory. Note: Docker requires absolute paths for binding mounts, so in this example we use `pwd` for printing the absolute path of the working directory, i.e. the `app` directory, instead of typing it manually
- `node:18-alpine` - the image to use. Note that this is the base image for our app from the Dockerfile
- `sh -c "yarn install && yarn run dev"` - the command. We're starting a shell using `sh` (alpine doesn't have `bash`) and running `yarn install` to install _all_ dependencies and then running `yarn run dev`. If we look in the `package.json`, we'll see that the `dev` script is starting `nodemon`.



