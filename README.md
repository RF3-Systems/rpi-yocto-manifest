# RF3 Raspberry Pi Yocto Manifest

Google repo manifest for the RF3 Raspberry Pi yocto project (Raspberry Pi 4, the lab jumpbox). Targets wrynose.

# Jump Start

1. Initialize and sync the sources:

```sh
mkdir rpi-yocto && cd rpi-yocto
repo init -u git@github-rf3:RF3-Systems/rpi-yocto-manifest.git -b wrynose
repo sync
```

2. Setup the yocto container to point to the sources on your local machine and build container:

```sh
cd sources/yocto-build-container
cp env.sample .env
nvim .env
# Change the *_PATH variables according to the README
make build-container
```

3. Enter the container and run bitbake:

```sh
make dev-entry
bitbake rf3-image                        # raspberrypi4-64 (default)
MACHINE=qemuarm64 bitbake rf3-image      # qemu
bitbake rf3-jumpbox-image                 # lab jumpbox, set its secrets in local.conf first
```

The distro, images and boot flow come from meta-rf3-distro, shared with the
other RF3 boards. The board itself is upstream meta-raspberrypi.
