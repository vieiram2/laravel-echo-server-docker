# laravel-echo-server-docker

Unofficial Dockerfile for the NPM package [laravel-echo-server](https://www.npmjs.com/package/laravel-echo-server),
based on [kylestev/laravel-echo-server-docker](https://github.com/kylestev/laravel-echo-server-docker).

## Configuration

Currently the Dockerfile expects a `laravel-echo-server.json` file mounted
onto the running container at the path: `/app/laravel-echo-server.json`.

To interactively generate a config file you can run the following command:

```
docker run -p 6001:6001 \
  -v /absolute/path/to/your/config.json:/app/laravel-echo-server.json \
  -i vieiram2/laravel-echo-server:1.3.2 init
```

Details about the options available in the configuration file can be found
on GitHub: [tlaverdure/Laravel-Echo-Server#configurable-options](https://github.com/tlaverdure/Laravel-Echo-Server#configurable-options).

## Running a container

Run the container with the standard laravel-echo-server port of `6001` exposed
from the echo-server instance running inside the container.

```
docker run -p 6001:6001 \
  -v /absolute/path/to/your/config.json:/app/laravel-echo-server.json:ro \
  -i vieiram2/laravel-echo-server:1.3.2 start
```

The `:ro` suffix on the volume flag (`-v`) specifies that the volume
(file in our case) will be read-only. If you do not wish to mount the config
file from the container's host machine (i.e. in production) you may want to
investigate the following:

- Create a volume to mount in place of the host machine volume mount
- Create a container with your configuration file in it and mount it

# Security

Make sure not to store your `laravel-echo-server.json` in a public GitHub repo.
