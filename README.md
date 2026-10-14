# Traffic Inbound

See and hear the X-Plane aircraft flown by a friend, in your own real sky.

A pilot flies in **X-Plane 12** on a Mac. **Traffic Inbound Gateway** (macOS) listens to the flight data X-Plane broadcasts and sends it, once per second, to a friend's iPhone or iPad through **Apple's Game Center**. **Traffic Inbound** (iOS) shows that aircraft on a radar, draws it in augmented reality where it really is, and plays its sound as if it were passing over you: engine of its type, propagation delay, Doppler shift, air absorption and, for a supersonic aircraft, the sonic boom.

| | |
|---|---|
| Marketing page | <https://www.mf-lab.com/Traffic-Inbound_MKTG.html> |
| Privacy policy | <https://www.mf-lab.com/Traffic-Inbound_Privacy-Policy.html> |
| Support | <https://www.mf-lab.com/support/> |

## Contents

- [What it does](#what-it-does)
- [Requirements](#requirements)
- [Quick start](#quick-start)
- [Setting up X-Plane](#setting-up-x-plane)
- [Troubleshooting](#troubleshooting)
- [How it is built](#how-it-is-built)
- [Build and test](#build-and-test)
- [Sounds and licences](#sounds-and-licences)
- [Privacy](#privacy)
- [Credits](#credits)

## What it does

- **Radar:** the aircraft around you, heading up or north up, with altitude, speed and a trail. The scale adapts from 500 m to 500 km. Each of six aircraft families has its own silhouette and colour (fighter, airliner, light aircraft, twin propeller, helicopter, glider).
- **AR camera:** the aircraft is drawn in the real sky, turned like the real one (heading, pitch, roll), with a halo, and a guidance arrow in the middle of the screen tells you where to turn the phone. The scene is aligned with true north.
- **Spatial sound:** the engine of the aircraft type, placed in 3D where the aircraft was when the sound left it. The sound arrives after the delay it needs (distance ÷ 343 m/s), its pitch follows the Doppler shift, distant aircraft lose their high frequencies, and the engine follows the N1 and the afterburner read from X-Plane.
- **Sonic boom:** a supersonic aircraft is silent while it approaches; when its shock wave (Mach cone) reaches you, a dry, low, loud boom plays in both ears.
- **Works anywhere:** the two devices find each other through Game Center. No router configuration, no accounts of our own.
- **Read-only:** the Gateway listens to X-Plane and only reads the aircraft type and the engine state. It never changes anything in the simulator.

## Requirements

| Who | What |
|---|---|
| Observer | iPhone or iPad, iOS 17.6 or later. An iPhone has the GPS, the compass and the camera the AR needs. A Wi-Fi-only iPad has no GPS, so radar and AR are less precise there. Headphones recommended. |
| Pilot | A Mac with macOS 14.6 or later, running X-Plane 12 (tested with 12.4.3) and Traffic Inbound Gateway on the same Mac. |
| Both | A Game Center account and an internet connection. **No VPN** while connecting (see Troubleshooting). |

## Quick start

**Pilot (Mac)**

1. In X-Plane, turn on the network output (see below).
2. Open **Traffic Inbound Gateway**. The *Flow* line says "active" as soon as X-Plane is flying.
3. Sign in to Game Center and click **Find match**.

**Observer (iPhone or iPad)**

1. Open **Traffic Inbound** and allow location (and the camera for AR).
2. Tap **Connect**: the app signs in to Game Center, finds the pilot and connects.
3. Look at the radar, tap **Open AR**, put on headphones, look up.

Both apps have an **Info** and a **Help** screen (the Mac has them in the toolbar and in the Help menu).

## Setting up X-Plane

In X-Plane 12: **Settings → Network → OTHER MAPPING APPS → "Broadcast to all mapping apps on the network"**. Do not choose "Transmit to a single mapping app".

That is all the Gateway needs: it listens on **UDP port 49002**, the one X-Plane uses for mapping apps. With *Identify the aircraft* on (the default) the Gateway also sends read requests (RREF) to X-Plane on `127.0.0.1:49000` for a few seconds every 30 s, to learn the aircraft and the engine state (N1, afterburner), then cancels them. In *Settings → Network → UDP PORTS* the port X-Plane receives on must stay at 49000.

If macOS asks whether the Gateway can receive incoming connections, choose **Allow**.

## Troubleshooting

| Symptom | What to check |
|---|---|
| Nothing arrives from X-Plane (*Flow: waiting for X-Plane*) | X-Plane is running with a flight loaded; the *Broadcast to all mapping apps* option is on; macOS firewall allows the Gateway; *Listening* says "UDP port 49002". |
| The devices pair but the connection drops, or never completes (*FastSyncTransportError*, "Socket is not connected") | **A VPN or network tunnel** on either device. Game Center can pair the players and then lose the data connection. Turn off any VPN, including apps with a built-in VPN, and reopen the app. In the iPhone log, `interface: utun…` on the `0.0.0.0:3030` flows gives it away. The app shows an orange warning when it sees a tunnel. |
| Generic aircraft on the iPhone | *Identify the aircraft* is on in the Gateway; X-Plane receives on port 49000. |
| No sound | The *Sound* button says "Sound on"; volume and headphones; a distant or idling aircraft is silent on purpose; a supersonic aircraft is silent while it approaches. |
| Direction is wrong in AR | Calibrate the compass (figure-of-eight movement) and stay away from metal. |
| The iPhone and the Gateway never find each other during development | Builds installed from Xcode use the Game Center *sandbox*; TestFlight and App Store builds use *production*. Both sides must be the same kind of build. |


## Privacy

No analytics, no advertising, no tracking, no accounts of our own, no servers. Your location is used only on your device to draw the radar and the AR view. The data that travels between the two devices is the position, attitude, type and engine state of the **simulated** aircraft, through Apple's Game Center. See the [privacy policy](https://www.mf-lab.com/Traffic-Inbound_Privacy-Policy.html).

## Credits

Traffic Inbound is an independent app by MF-Lab. X-Plane is a trademark of Laminar Research; this project is not affiliated with or endorsed by Laminar Research. Apple, iPhone, iPad, Mac and Game Center are trademarks of Apple Inc.

© 2026 MF-Lab.com
