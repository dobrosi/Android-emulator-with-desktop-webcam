# Create Desktop webcam for Android emulator.
## Install fakecam for Linux.
### Install v4l2loopback application.
```
sudo apt install v4l2loopback-dkms
```
### Configure fakecam.
Create /etc/modprobe.d/linux-fake-background.conf file.
```
sudo vim /etc/modprobe.d/linux-fake-background.conf
```
Copy this content to linux-fake-background.conf file:
```
options v4l2loopback devices=1 exclusive_caps=1 video_nr=0 card_label="desktop-cam"
```
Restart systemd-modules-load
```
systemctl restart systemd-modules-load.service
```
Fake cam is ready.
## Create desktop share as a webcam.
### Install ffmpeg application.
```
sudo apt install ffmpeg
```
### Start sharing as virtual webcam.
```
sudo ffmpeg -probesize 100M -framerate 15 -f x11grab -video_size 1280x720 -i :0.0+0,0 -vcodec rawvideo -pix_fmt yuv420p -f v4l2 /dev/video0
```
## Run emulator with prepared virtual webcam
```
emulator -camera-back webcam1 -camera-front webcam1 -no-snapshot -avd Pixel_API_30
```
Ready.
# Useful links:
1. https://github.com/fangfufu/Linux-Fake-Background-Webcam/tree/master
2. https://wiki.archlinux.org/title/V4l2loopback
