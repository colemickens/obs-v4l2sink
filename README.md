## colemickens fork info

This is a lightly maintained fork, with these applied:

- https://github.com/CatxFish/obs-v4l2sink/pull/21 (cc: @treister)
- https://github.com/CatxFish/obs-v4l2sink/pull/35 (cc: @jktjkt)
- https://github.com/CatxFish/obs-v4l2sink/pull/58 (cc: @yetist)
- https://github.com/CatxFish/obs-v4l2sink/pull/59 (cc: @yetist)
- https://github.com/CatxFish/obs-v4l2sink/pull/61 (cc: @aleixpol)

Credit to their respective authors.

(Note, as of this second, I think one of them might be breaking something. No devices appear in the OBS dropdown.)

**If you use this please open an issue or comment in an existing one!**

I'm not really a C expert, I'm not dying to maintain this, but also I don't want to keep applying a bunch of patches.

---

# obs-v4l2sink

An [OBS Studio][obs-proj] plugin that provides output capabilities to a
Video4Linux2 device. It is basically a Linux version of [obs-virtual-cam][vcam],
but only contains the video sink part. You can use it with
[v4l2loopback][v4l2loopback] to achieve cross-program video transfer between OBS
Studio and third party software supporting Video4Linux2, e.g. to present an OBS
session in proprietary browser-based conferencing systems by selecting the OBS
session as a webcam.

The idea for this plugin originated from the discussions around [obs-virtual-cam
issue #17][vcam#17].

[obs-proj]: https://obsproject.com/
[vcam]: https://github.com/CatxFish/obs-virtual-cam
[v4l2loopback]: https://github.com/umlaeute/v4l2loopback
[vcam#17]: https://github.com/CatxFish/obs-virtual-cam/issues/17

## Usage with v4l2loopback

- Make sure to [load the v4l2loopback module][run-v4l2loopback] and check the Device Path.
  - If using Chrome or Chromium you must use the option `exclusive_caps=1`.
- Open OBS and select the menu entry `Tools > V4L2 Video Output`.
- Fill in the Device Path and select the appropriate video format.
- Click the `Start` button.

![Property Window](docs/property-window.png)

[run-v4l2loopback]: https://github.com/umlaeute/v4l2loopback#run

## Build

- Install QT

```
sudo apt install qtbase5-dev
```

- Get obs-studio source code

```
git clone --recursive https://github.com/obsproject/obs-studio.git
```

- Build plugins

```
git clone https://github.com/CatxFish/obs-v4l2sink.git
cd obs-v4l2sink
mkdir build && cd build
cmake -DLIBOBS_INCLUDE_DIR="../../obs-studio/libobs" -DCMAKE_INSTALL_PREFIX=/usr ..
make -j4
sudo make install
```
