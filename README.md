# 3d2png

Update with three.js 162. The last Version of three.js with support of for WebGL 1. The software 3d2png depends on headless-gl, which only supports WebGL 1.

**Remarks: Standard light system RoomEnvironment is not working with headless rendering. The patch of PMREMGenerator to get RoomEnvironment to work did not work for all systems. An attempt was made here to imitate RoomEnvironment with classic lights. It must be checked whether this is sufficient.**

Test: node --inspect 3d2png.js samples/DavidStatue.stl 640x480 test.png

![DavidV88](samples/DavidStatue.png)

Rendering of the image with the old lightning system of v88.

No lights after the update to v162. Lightning system changed with v152.

![DavidV162](samples/DavidStatue_room_environment_like.png)

Rendering of the image with v162 and adapted light system to mimic RoomEnvironment.

![DavidV162](samples/DavidStatue_room_environment.PNG)

Rendering of the image with v162 and Standard light system RoomEnvironment in the new 3D Extension: https://opendem.github.io/WikiMediaExtension3D_Test_GLB_Format/


## How to build 3d2png-deploy

Simple thumbnail generator for AMF and STL files. It tries to pick a reasonable
camera position based on the bounding box of the geometry.

## How to build 3d2png-deploy

The deploy repository needs to be built on a system as similar to the
production hosts as possible. For this reason, we use the service-runner
package, which spins up a Docker container based on the definition
provided in the `deploy` stanza of package.json, installs the
distribution packages needed, builds the node_modules directory and
updates the source repo submodule.

To that end, this commit adds the deployment definition to package.json
and service-runner as a development dependency (which means it will not
get installed into the deploy repository). There is also a minimal
config.yaml file that is needed by service-runner in order to build the
deploy repository.

Note that in order for the build process to work you need Docker set up
on the machine, as well as configure git to point to the location of the
deploy repository:

    $ git config deploy.dir /full/path/to/deploy/repo

The build process can then be initiated with

    $ npm run build-deploy
