# iPadAir-HA

A native wall panel for Home Assistant controls and camera monitoring, built for a first-generation iPad Air running iOS 12.5.8.

## Project status

Research and planning. No application code exists yet, and playback has not been tested on the iPad.

## Planned app

- Swift and UIKit with an iOS 12 deployment target.
- Landscape layout with large controls for favourite lights, scenes, and sensor readings.
- Camera thumbnails with tap-to-open live video.
- Connection status, stale-data indicators, and automatic network reconnection.
- Dim idle screen and support for use with Guided Access.
- Credentials stored in Keychain, never in the repository.

## Integration plan

Home Assistant OS runs in a VM on TrueNAS. Scrypted runs as a Home Assistant add-on and provides camera feeds from an Ajax NVR.

The app will use Home Assistant's APIs directly rather than render a Lovelace dashboard. Camera playback will use AVPlayer with an H.264 HLS stream.

First, test Scrypted rebroadcast feeds through Home Assistant camera entities and HA's HLS output. If that route is unsuitable, evaluate a go2rtc add-on or another video bridge. HomeKit is not the planned camera transport because updated Apple Homes require iOS 16.2 or later.

Stream compatibility, startup delay, simultaneous feed capacity, and overnight reliability remain unverified.

## Build environment

The intended build environment is Xcode 15.4 on macOS Sonoma 14, with installation on a registered iPad using an Apple Developer Program account. Physical-device testing is required. Signed builds require periodic provisioning renewal.

## First milestone

1. Build and install a minimal signed UIKit app on the iPad.
2. Display one live HA sensor and control one light.
3. Play one camera stream and measure startup time and viewing delay.
4. Test recovery after Wi-Fi interruption and app backgrounding.
5. Run an overnight stability test before expanding the dashboard.

The homelab console and CNC workshop companion are possible later projects. The first release focuses on the HA wall panel and cameras.

## References

- [Home Assistant REST API](https://developers.home-assistant.io/docs/api/rest/)
- [Home Assistant WebSocket API](https://developers.home-assistant.io/docs/api/websocket/)
- [Home Assistant camera implementation](https://github.com/home-assistant/core/blob/dev/homeassistant/components/camera/__init__.py)
- [Scrypted rebroadcast implementation](https://github.com/koush/scrypted/blob/main/plugins/prebuffer-mixin/src/main.ts)
- [go2rtc HLS implementation notes](https://github.com/AlexxIT/go2rtc/blob/master/internal/hls/README.md)
- [Apple Xcode compatibility](https://developer.apple.com/xcode/system-requirements)
- [Apple registered-device distribution](https://developer.apple.com/documentation/xcode/distributing-your-app-to-registered-devices)
- [Apple Home compatibility](https://support.apple.com/en-za/102287)
