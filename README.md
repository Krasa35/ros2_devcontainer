#   ROS2 devcontainer
![Static Badge](https://img.shields.io/badge/noetic-building-brightgreen)
![Static Badge](https://img.shields.io/badge/humble-building-brightgreen)
![Static Badge](https://img.shields.io/badge/jazzy-building-brightgreen)
## ROS2 version change
In order to run the container on a different ROS2 version, you need to change current branch on Github and rebuild the container.
## How to run
1. Install Docker and VSCode.
2. Make sure you can run Docker without sudo. (e.g. `docker run hello-world`)
3. Clone the repository.
4. Open the repository in VSCode. (main tree needs to contain `.devcontainer` folder)
5. Install the [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension.
6. Click on the Poup in the bottom right corner of the VSCode window. (or press `Ctrl+Shift+P` and type `Dev Containers: Reopen in Container`)
7. Wait for the container to build and start.
8. You are now in the container. You can run ROS2 commands in the terminal. You don't have to source your workspace and `/opt/ros/$ROS_DISTRO/setup.bash` it is sourced by default.

## Troubleshooting
In case of below error:
```bash
Authorization required, but no authorization protocol specified

qt.qpa.xcb: could not connect to display :1
qt.qpa.plugin: Could not load the Qt platform plugin "xcb" in "" even though it was found.
This application failed to start because no Qt platform plugin could be initialized. Reinstalling the application may fix this problem.

Available platform plugins are: eglfs, linuxfb, minimal, minimalegl, offscreen, vnc, xcb.

Aborted (core dumped)
```
Please allow the container to access the X server by running the following command:
```bash
xhost +local:root
```

In case of not building the container, ensure all mounts source path is valid and accessible.

Make sure permissions granted to the user inside docker container are fulfilling your needs.

## NVidia GPU support
If you have NVidia GPU and want to use it in the container, you need to install the NVidia drivers on the host machine and then run the container with the following uncommented commands in devcontainer.json:
```json
    "runArgs": [
        "--net=host",
        "--gpus=all",
        "--runtime=nvidia",
        "-e",
        "DISPLAY=:1"
    ],
```
