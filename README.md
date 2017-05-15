# docker-varnish
Dockerized Varnish.

## Build

    $ chmod +x ./build.sh
    $ ./build.sh

## Prepare
- A folder where all container configuration data stored, in example "**varnish-container**".
- "**varnish-container/conf.d**" folder to provide additionals configuration.

Create "**nginx-container/conf.d/default.vcl**" file and put below content.

    vcl 4.0;
    
    backend default {
        .host = "<your_backend_host>";
        .port = "<your_backend_port>";
    }
    
    acl purge {
        "<your_backend_host>";
    }

## Run

    docker run --interactive --tty --name=varnish --memory=512m \
    --hostname=varnish \
    --volume=/path/to/varnish-container/conf.d:/etc/varnish \
    --publish="6081:6081" \
    --detach \
    varnish:5.1.2

## Environment Defaults
    VARNISH_VERSION=5.1.2
    VARNISH_PORT=6081
    VARNISH_MEMORY=100m