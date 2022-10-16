# Disclaimer

| !IMPORTANT! | This is a development branch, that is not relelased by CompuLab officially yet|
|---|---|

# Configuring the build

## Setup Yocto environment

* WorkDir:
```
mkdir compulab-nxp-bsp && cd compulab-nxp-bsp
```
* Set a CompuLab machine:

| Machine | Command Line |
|---|---|
|ucm-imx8m-plus|```export MACHINE=ucm-imx8m-plus```|
|som-imx8m-plus|```export MACHINE=som-imx8m-plus```|
|iot-gate-imx8plus|```export MACHINE=iot-gate-imx8plus```|
|sbc-iot-imx8plus|```export MACHINE=iot-gate-imx8plus```|

## Initialize repo manifests

* NXP
```
repo init -u https://source.codeaurora.org/external/imx/imx-manifest -b imx-linux-kirkstone -m imx-5.15.32-2.0.0.xml
```

* CompuLab
```
mkdir -p .repo/local_manifests
wget --directory-prefix .repo/local_manifests https://raw.githubusercontent.com/experientials/meta-bsp-929/kirkstone/scripts/meta-bsp-929.xml
```

* Sync Them all
```
repo sync
```


## Setup build environment

* Initialize the build environment:
```
source compulab-setup-env -b build-${MACHINE}
```
* Building the image:
```
bitbake -k imx-image-multimedia
```

## Deployment
### Create a bootable sd card

* Goto the `tmp/deploy/images/${MACHINE}` directory:
```
cd tmp/deploy/images/${MACHINE}
```

* Deploy the image:
```
sudo bmaptool copy imx-image-multimedia-${MACHINE}.wic.bz2 --bmap imx-image-multimedia-${MACHINE}.wic.bmap /dev/sdX
```

### Camera Support patched in

- IMX477 1/2.3" 12MP 4:3 DOL-HDR
- AR0234
- AR0521 1/2.5" 5MP 4:3 y-2020
- AR1335


