# seagull

Checking Docker containers across hosts can mean switching between terminals just to find a container or stop it. seagull provides a web interface for those tasks, with container and image controls in one place.

## Features

- Start, stop, and delete Docker containers from the browser.
- Delete Docker images through the web interface.
- Search and filter the container and image lists.
- Manage and monitor Docker resources across multiple hosts.
- Use the interface in English, Chinese, German, or French.

## Installation

You need a running Docker daemon. The example below also requires Node.js and uses JavaScript to pull the upstream container image:

```sh
node --input-type=module <<'JS'
import { execFileSync } from 'node:child_process';

execFileSync('docker', ['pull', 'tobegit3hub/seagull'], {
  stdio: 'inherit'
});
JS
```

This standalone project is based on tobegit3hub/seagull. The image above is the upstream distribution, not a separately published image for this project. Although the web interface uses JavaScript, the upstream application also has a Go backend; it is not an npm-only application.

## Usage

Run the upstream application with access to the local Docker socket:

```sh
docker run -d --name seagull -p 127.0.0.1:10086:10086 -v /var/run/docker.sock:/var/run/docker.sock tobegit3hub/seagull
```

Open `http://127.0.0.1:10086` in your browser. Use the container list to find a container, inspect its state, and start or stop it. The image list provides controls for deleting images.

**Docker socket access grants control over the host's Docker daemon.** Keep the interface bound to localhost unless you have configured appropriate access controls. Do not expose an unauthenticated Docker API to enable multi-host access.

To stop and remove the web interface container:

```sh
docker stop seagull
docker rm seagull
```

## License

Licensed under Apache-2.0. This project is based on [tobegit3hub/seagull](https://github.com/tobegit3hub/seagull). Preserve the upstream copyright and license notices, and retain any applicable NOTICE file when redistributing derived code.
