# FreqMapper

**Discover and help map real-world Meshtastic coverage.**

FreqMapper is a community coverage-mapping service for Meshtastic. It helps answer a practical question: *can the mesh reach this trail, road, neighborhood, or valley?*

The Android and iPhone apps connect to your Meshtastic radio over Bluetooth and use your phone's GPS to record coverage tests and received activity. The public website brings those results together into regional maps.

**New here? Start with the [public map](https://freqmapper.net/) or the [getting started guide](https://help.freqmapper.net/getting-started/).** This GitHub repository is the public place for bug reports, feature requests, and community feedback.

## Official links

| I want to… | Go here |
| --- | --- |
| Explore the map and find a region | [FreqMapper website](https://freqmapper.net/) |
| Install on Android | [FreqMapper Wardriving on Google Play](https://play.google.com/store/apps/details?id=net.freqmapper.app) |
| Install on iPhone | [FreqMapper Wardriving on the App Store](https://apps.apple.com/app/id6806389954) |
| Follow setup instructions | [Getting started](https://help.freqmapper.net/getting-started/) |
| Browse guides and answers | [FreqMapper Help](https://help.freqmapper.net/) |
| Ask the community for help or an enrollment code | [FreqMapper Wardriving Discord](https://discord.gg/mccXD4qvgD) |
| Report a bug or suggest a feature | [Open a feedback issue](https://github.com/Littleaton/FreqMapper-Feedback/issues/new/choose) |

Ordinary installation uses the public app-store links above. Follow the [tester instructions](https://help.freqmapper.net/getting-started/#get-the-app) only when a beta announcement asks you to.

## What can I do with FreqMapper?

- **Explore regional coverage** in a browser before planning a trip.
- **Map with Active Patrol (TX + RX):** send paced mapping tests and record eligible traffic your radio receives, where regional policy permits.
- **Map with Silent Recon (RX only):** record eligible received traffic without sending FreqMapper mapping tests.
- **Check one spot with Test signal here:** request a manual signal test without starting a wardrive or recording a route.
- **Help your local mesh grow:** contribute measurements or work with your regional team to connect an existing Watcher.

A **Watcher** is an independent MQTT gateway that reports packets it received over radio. A controlled mapping test becomes **verified TX coverage** when an approved Watcher independently reports the matching packet. **Received here / passive RX** records what your driving radio heard at your phone's location and remains a separate kind of evidence.

Packets can travel through mesh relays, so a Watcher receipt does not prove a direct radio link. Read the [map guide](https://help.freqmapper.net/using-the-public-map/) and [complete legend](https://help.freqmapper.net/map-legend/) to understand the results.

## Get set up

You need a supported Android phone or iPhone, a Bluetooth-capable Meshtastic radio, Bluetooth and precise-location permissions, and internet access for initial setup. See [recommended hardware](https://help.freqmapper.net/recommended-hardware/) if you still need a radio.

1. **Find your area and get an enrollment code.** Check the [public map](https://freqmapper.net/) for an active region. Ask your regional team or [Discord community](https://discord.gg/mccXD4qvgD) for a current code. It enrolls your connected radio; it is separate from a Meshtastic channel key and should stay private.
2. **Install the app.** Use Google Play or the App Store above.
3. **Connect your radio.** Allow the requested Bluetooth and precise-location access. Open **Radio**, select your Meshtastic radio, and wait for its identity and channels to finish loading.
4. **Enroll and prepare the radio.** Apply the enrollment code while connected, then follow the app's setup prompts. The default mapping setup adds or reuses a shared channel in a free secondary slot without replacing your configured channels. Follow the [radio enrollment](https://help.freqmapper.net/join-a-mapping-region/) and [app setup](https://help.freqmapper.net/set-up-the-app/) guides.
5. **Link your profile for history and recovery.** Open **Settings → Profile & data** and choose **Sign in and link this app**. Website sign-in alone does not link the phone app.
6. **Make your first measurement.** On the Map, confirm your GPS position, region, radio readiness, and Watcher activity. Expand **WarDrive** and choose **Active Patrol** or **Silent Recon**, or use **Test signal here** for a single spot test. A region may allow only Silent Recon.

Follow [Your first mapping trip](https://help.freqmapper.net/first-mapping-trip/) for the full workflow, including offline preparation. Set up before driving and have a passenger operate the app when possible.

## No FreqMapper region near you?

Read [Start a FreqMapper region](https://help.freqmapper.net/start-a-region/) and [Help grow the map](https://help.freqmapper.net/help-grow-the-map/), then talk with your local mesh team and the Discord community. Regional onboarding is coordinated with the team rather than self-service. Verified coverage needs approved, independently listening Watchers; installing the app alone does not establish regional coverage.

## Get help or send feedback

Start with [Troubleshooting](https://help.freqmapper.net/troubleshooting/), the [FAQ](https://help.freqmapper.net/frequently-asked-questions/), or [Discord](https://discord.gg/mccXD4qvgD).

For bugs and feature ideas, [search existing issues](https://github.com/Littleaton/FreqMapper-Feedback/issues) before opening a [new report](https://github.com/Littleaton/FreqMapper-Feedback/issues/new/choose). Include what you expected, what happened, steps to reproduce, your app version, phone/OS or browser, and relevant radio model and firmware. For a feature request, explain the problem you want to solve.

You can also report from **Settings → Help & about → Report a bug / Request a feature** in the app. Choose **Public summary** for a public discussion or **Private report** for private support. For private support, account, or privacy questions, see the [Support guide](https://help.freqmapper.net/support/) or email [support@freqmapper.net](mailto:support@freqmapper.net).

**Everything posted directly to this GitHub tracker is public.** Never post enrollment codes, channel keys or QR codes, passwords, tokens, broker credentials, private messages, Bluetooth addresses, or precise private locations. Review screenshots and logs before sharing. Read [Privacy and reporting](PRIVACY_AND_REPORTING.md) and the [Privacy Policy](https://help.freqmapper.net/privacy/) for details.

## About this repository

This repository hosts community feedback and public discussion. The application source and operational configuration are maintained separately. You can use FreqMapper through the website and mobile apps without cloning or building anything here.
