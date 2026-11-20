# FreqMapper

**Find out where your Meshtastic mesh actually reaches—and help fill in the map.**

FreqMapper is a community service for measuring and sharing real-world **Meshtastic coverage**. The Android and iPhone apps connect to your radio, use your phone's GPS, and collect evidence while you travel or test a single spot. The website brings that evidence together into regional maps that anyone can explore.

It is for the person looking at a trailhead, back road, neighborhood, or valley and wondering: *would the mesh make it from here?*

[Explore the map](https://freqmapper.net/) · [Get started](https://help.freqmapper.net/getting-started/) · [Android](https://play.google.com/store/apps/details?id=net.freqmapper.app) · [iPhone](https://apps.apple.com/app/id6806389954) · [Join Discord](https://discord.gg/mccXD4qvgD)

![A FreqMapper trip: a phone, a radio, and independently observed coverage across a valley.](https://help.freqmapper.net/assets/freqmapper-wardriving-v1.png)

**This is FreqMapper's public feedback repository.** You are welcome to read, ask questions, report bugs, suggest features, and follow public discussions here. To use FreqMapper, start with the website and mobile apps; there is nothing you need to clone or build from this repository.

## Find what you need

| I want to… | Start here |
| --- | --- |
| See the map and find my local mesh | [FreqMapper public map](https://freqmapper.net/) |
| See an established community map | [Explore the Freq51 map](https://freq51.freqmapper.net/) |
| Install on Android | [Google Play](https://play.google.com/store/apps/details?id=net.freqmapper.app) |
| Install on iPhone | [App Store](https://apps.apple.com/app/id6806389954) |
| Set up my first radio and trip | [Getting started](https://help.freqmapper.net/getting-started/) |
| Ask about enrollment or bringing my area onboard | [FreqMapper Wardriving Discord](https://discord.gg/mccXD4qvgD) |
| Read the full documentation | [FreqMapper Help](https://help.freqmapper.net/) |
| Manage my linked apps, radios, trips, and account | [My profile](https://freqmapper.net/profile) |
| See mapping contributions | [Leaderboards](https://freqmapper.net/leaderboard) |
| Find out what changed | [Product release notes](https://help.freqmapper.net/releases/) and [mobile releases](https://help.freqmapper.net/app-release-history/) |
| Report a problem or suggest an idea | [Feedback issues](https://github.com/Littleaton/FreqMapper-Feedback/issues) |
| Get private support | [Support guide](https://help.freqmapper.net/support/) or [support@freqmapper.net](mailto:support@freqmapper.net) |

### On this page

- [What FreqMapper is and why it exists](#what-freqmapper-is-and-why-it-exists)
- [What you can do](#what-you-can-do)
- [How the coverage evidence works](#how-the-coverage-evidence-works)
- [How to read the map](#how-to-read-the-map)
- [Get set up](#get-set-up)
- [Manual tests, offline mapping, and background use](#manual-tests-offline-mapping-and-background-use)
- [The mobile apps](#the-mobile-apps)
- [Profiles, trips, sharing, and leaderboards](#profiles-trips-sharing-and-leaderboards)
- [Regions, Watchers, and local mesh teams](#regions-watchers-and-local-mesh-teams)
- [Discord and other integrations](#discord-and-other-integrations)
- [Privacy and control over your data](#privacy-and-control-over-your-data)
- [Support, feedback, and contributing](#support-feedback-and-contributing)
- [Complete public guide directory](#complete-public-guide-directory)
- [About the project and this repository](#about-the-project-and-this-repository)

## What FreqMapper is and why it exists

FreqMapper grew out of a practical need at **Freq51**: we wanted to see where our mesh actually reached. Community mapping tools provided inspiration, and we wanted an app we could start before a drive and leave running in the background. FreqMapper was built from scratch around that workflow.

The result is one shared service with local regions, native mobile apps, a public web map, and independent receiving gateways that help confirm what was heard.

FreqMapper works with **[Meshtastic](https://meshtastic.org/)**, the open-source radio mesh ecosystem. Your own Meshtastic radio provides the radio link; your phone supplies the app, location, and connection to FreqMapper. You do not need to understand MQTT or operate a server to become a mapper.

Different people can take part in different ways:

| If you are… | FreqMapper can help you… |
| --- | --- |
| Curious about your local mesh | Explore measured coverage, regional information, and Watchers in a browser. |
| A radio owner | Contribute measurements during a trip or test an individual location. |
| On a busy mesh | Use receive-only mapping to record where your radio hears eligible traffic without adding mapping-test packets. |
| A local mesh operator | Bring together coverage evidence, coordinate a region, and connect existing receiving gateways. |
| Building another application | Request an approved integration that keeps verified TX and passive RX evidence distinct. |

Coverage is a record of observations under real conditions. Equipment, terrain, antenna placement, mesh activity, and the available Watchers all affect results. Read it as evidence for planning, with the limitations explained in the [map guide](https://help.freqmapper.net/map-guide/).

## What you can do

### Choose how you map

| Mode or action | What it does | When it is useful |
| --- | --- | --- |
| **Active Patrol — TX + RX** | Sends paced, controlled mapping tests and records eligible traffic received by your radio. | Measuring where your transmissions can reach the mesh, where regional policy permits. |
| **Silent Recon — RX only** | Records eligible traffic your radio hears without sending FreqMapper mapping tests. | Exploring reception, especially on busy meshes or in regions with receive-only policies. |
| **Test signal here** | Requests one controlled test at your current GPS position without requiring a wardrive or route recording. | Checking a trailhead, campsite, building entrance, or other specific spot. |

Silent Recon is receive-only for FreqMapper mapping activity; the radio's own normal Meshtastic configuration still applies. Stop Silent Recon before requesting a manual transmission. Regional receive-only restrictions also apply to manual tests.

### Explore, review, and improve

- Browse public regional maps, Watcher details, mesh information, and activity.
- Review your own saved trips, test results, and received-here evidence.
- Link Android and iPhone installations to one profile.
- Share a finished trip's coverage through an optional, revocable link.
- Track verified mapping contributions and separate RX exploration totals.
- Help fill unmeasured areas or revisit existing coverage with careful, well-spaced tests.
- Work with the community to establish a region or connect an existing Watcher.

Features and small interface details can vary by installed release and regional policy. Use the [mobile release history](https://help.freqmapper.net/app-release-history/) and [settings reference](https://help.freqmapper.net/mobile-app-settings/) for current details.

## How the coverage evidence works

For a controlled mapping test:

1. **Your phone records the test location** from its current GPS fix.
2. **Your connected radio sends the identified test** using its approved mapping configuration.
3. **An independent approved Watcher receives the packet over radio** and reports its receipt through MQTT.
4. **FreqMapper matches the receipt to the test.**
5. **The matching result contributes verified TX coverage** at the test location.

A **Watcher** is the independent Meshtastic MQTT gateway that received and reported a packet. It is not automatically the sender, the driving radio, or a mesh repeater. A Watcher's Meshtastic device role can vary.

### Three useful kinds of evidence

| Evidence | What it tells you | Where the location comes from | Contribution credit |
| --- | --- | --- | --- |
| **Verified TX coverage** | An approved independent Watcher heard a controlled FreqMapper mapping test. | The mapper's phone GPS when the test was sent. | Eligible for verified TX contributions. |
| **Position Packet coverage** | An approved Watcher heard a normal Meshtastic Position Packet over RF. | The position reported by the sending node. | Separate from controlled tests; no mapper credit. |
| **Received here / passive RX** | The driving radio heard eligible traffic at that location. | The driving phone's GPS at reception time. | Separate RX exploration totals; never verified TX credit. |

Received-here evidence can include eligible text, position, node-info, and telemetry packets. FreqMapper records limited reception metadata; the RX mapping record does not upload message text.

A test dot or a radio queue acknowledgement is not yet verified TX. A relay acknowledgement is also insufficient. Verification requires the independent approved Watcher receipt.

Multiple Watchers add independent observations, but they do not reveal the complete RF route. Packets may pass through relays, and a Watcher's RSSI/SNR describes its received final hop. Lines between a test and a Watcher visualize the evidence relationship, not a proven direct radio path.

Read [How FreqMapper works](https://help.freqmapper.net/how-freqmapper-works/), [Received here and passive RX](https://help.freqmapper.net/received-here/), and the [glossary](https://help.freqmapper.net/glossary/) for the full explanation.

## How to read the map

The public map brings regional evidence together while keeping the evidence types distinguishable.

| Standard appearance | Meaning |
| --- | --- |
| **Green / strong TX** | Independently heard controlled tests with strong evidence. |
| **Yellow / fair TX** | Independently heard controlled tests with more limited evidence. |
| **Orange / weak TX** | Weak signal or limited independent confirmation. |
| **Amber / degraded** | Previously established TX coverage challenged by credible newer completed misses. |
| **Red / not heard** | A credible completed test was not independently heard, or repeated credible misses challenged established coverage. |
| **Purple RX** | Eligible traffic was heard by a driving radio in that area. Darker purple means stronger receive evidence. |
| **Position Packet cells** | Normal Position Packet coverage, identified with a dashed outline. |
| **Neutral / no fill** | Unmeasured area. It does not mean a failed test. |
| **Eye marker** | An approved Watcher with a usable public position. |

Some Watchers can verify packets without appearing as eye markers because a usable public position is unavailable.

Coverage does **not** fade merely because it is old. Credible newer testing can challenge it. The public view prioritizes positive verified TX, then Position Packet coverage, then purple RX, while retaining the underlying evidence separately.

The map uses approximately **300 m overview cells** and **100 m detail cells**. Their physical size varies with latitude. A colored cell summarizes observations; it does not promise the same reception at every point inside it. Regional boundaries organize the map and local policy rather than defining an RF wall.

Accessible and monochrome palettes, outlines, and patterns help distinguish evidence without relying only on the standard colors. Mobile maps also show your current trip's route and private test/RX markers, which differ from the shared public cells.

Start with [Using the public map](https://help.freqmapper.net/using-the-public-map/) and keep the [complete map legend](https://help.freqmapper.net/map-legend/) nearby.

## Get set up

### What you need

- A supported Android phone or iPhone.
- A compatible Meshtastic radio and antenna appropriate for your local frequency band.
- A working connection between the phone and radio; Bluetooth is the usual starting point.
- Precise-location permission and a fresh phone GPS fix.
- Internet for first-time registration, enrollment, and initial radio preparation.
- A current FreqMapper enrollment code.
- An active FreqMapper region and the regional mapping policy for the area you want to measure.
- Approved, independently listening Watchers for verified TX results.

Read [Recommended hardware](https://help.freqmapper.net/recommended-hardware/) before buying equipment. For initial Meshtastic setup, use the [official Meshtastic getting-started documentation](https://meshtastic.org/docs/getting-started/). The radio must already use the appropriate LoRa region and local mesh settings.

### Install the app

| Platform | Normal installation | Announced beta testing |
| --- | --- | --- |
| **Android** | [Google Play](https://play.google.com/store/apps/details?id=net.freqmapper.app) | Follow the [tester guide](https://help.freqmapper.net/getting-started/#get-the-app). If instructed to use closed testing, join the [beta testers Google Group](https://groups.google.com/g/freqmapper-beta-testers/) with your Play account, then [accept the test](https://play.google.com/apps/testing/net.freqmapper.app). |
| **iPhone** | [App Store](https://apps.apple.com/app/id6806389954) | For an announced beta, use Apple's TestFlight app and the [FreqMapper TestFlight invitation](https://testflight.apple.com/join/RkMXhuXg). |

Ordinary public installation does not require joining the Android closed-test group or using TestFlight. Store eligibility, processing, and rollout timing can affect availability. The [mobile releases page](https://help.freqmapper.net/app-release-history/) links to the documented public and tester histories.

### First-use walkthrough

1. **Check the map.** Open [freqmapper.net](https://freqmapper.net/) and find your area. If your mesh is missing, join [FreqMapper Discord](https://discord.gg/mccXD4qvgD) to discuss onboarding.
2. **Get a current enrollment code.** Ask in FreqMapper Discord. It enrolls a connected radio into FreqMapper; it is separate from a Meshtastic channel key. Keep the code private.
3. **Install and open FreqMapper.** Allow the Bluetooth, connection, and precise-location permissions your phone requests.
4. **Connect in Radio.** Choose your radio and wait for its identity and channels to finish synchronizing. Keep other apps and phones disconnected from that radio while FreqMapper is using it.
5. **Apply the enrollment code while connected.** Confirm the intended radio, then follow the app's preparation prompts.
6. **Link your profile if you want account history and recovery.** Open **Settings → Profile & data → Sign in and link this app**. Signing in on the website alone does not link the phone.
7. **Check readiness on the Map.** Confirm the GPS position, selected region, radio status, mapping configuration, and Watcher activity.
8. **Start intentionally.** Expand **WarDrive** and choose **Active Patrol** or **Silent Recon**. For one location, use **Test signal here** when transmission is allowed.
9. **Review and finish.** Use **Activity** to inspect progress and **Trips** to review a completed session. End the wardrive when you are done and let waiting uploads finish.

An enrolled radio can map in other active regions. Your current phone location determines the applicable regional policy; the code's issuing region does not lock your radio to that area.

Follow the complete [getting-started path](https://help.freqmapper.net/getting-started/), [radio enrollment guide](https://help.freqmapper.net/join-a-mapping-region/), [app setup guide](https://help.freqmapper.net/set-up-the-app/), and [first-trip guide](https://help.freqmapper.net/first-mapping-trip/).

### What happens to my radio configuration?

The default Active Patrol setup uses a managed FreqMapper channel in an available secondary slot. The app adds or reuses the approved channel and does not overwrite your primary channel or an occupied secondary slot. It does not automatically change your LoRa region, modem preset, or unrelated MQTT settings.

If there is no free secondary slot, review the setup guide before deciding whether to free one. Channel names, keys, and provisioning QR codes are private; the app retrieves its approved configuration through enrollment.

Configured radios can instead use primary-channel **Telemetry HostMetrics** or **PRIVATE_APP** mapping tests. Follow the app's effective configuration and regional instructions. Silent Recon does not need to send tests through the managed channel.

## Manual tests, offline mapping, and background use

### Test one spot

**Test signal here** can send a controlled test without starting a wardrive or recording a route. It has a separate 30-second cooldown and allows up to three attempts in a rolling five-minute period in the same 100 m cell. It also works while stationary.

During Active Patrol, a manual request uses the next safe transmission slot ahead of the automatic test. It still needs valid authorization, a ready enrolled radio, and fresh, accurate GPS. Regional receive-only restrictions remain in effect.

See [manual signal tests](https://help.freqmapper.net/first-mapping-trip/#4-use-automatic-tests-or-test-signal-here).

### Prepare for missing phone internet

Bluetooth or another local radio connection and phone GPS can keep working without cellular data. Once properly prepared, the app can save supported trip records in an encrypted upload queue and send them when internet returns. An independent Watcher still needs to deliver the receipt needed for TX verification.

Offline starting permissions differ:

- **Silent Recon:** a previously configured app can record receive-only sessions with the required radio and valid location context.
- **Active Patrol:** an offline start needs valid saved approval for the radio, area, and managed channel. Automatic primary-channel tests require live authorization.
- **Manual spot tests:** separate saved offline permission can cover the configured transport. Prepare online and check the **Offline tests ready** area and expiry before leaving.

Manual permission normally lasts up to 72 hours, although a scheduled configuration change can shorten it. New manual results must upload within seven days after that permission expires. Uploading a saved result does not send another radio test. Review the [offline test workflow](https://help.freqmapper.net/first-mapping-trip/#test-in-an-area-without-internet) before relying on it.

### Keep a trip running while using the phone

Changing FreqMapper tabs does not stop a trip. Background recording and radio activity remain subject to Android and iOS permissions and execution rules. Returning to the map refreshes the display; force-quitting the app or operating-system termination is not guaranteed background operation.

Optional **Connect radio when app opens** and **Start wardrive after automatic connection** are separate settings, both off by default. Complete a successful manual setup before enabling them. See [automatic startup settings](https://help.freqmapper.net/mobile-app-settings/#automatic-connection-and-wardrive-start).

Set up while parked, respect local radio practices, and have a passenger operate the app when interaction would distract the driver.

## The mobile apps

Android and iPhone share the same main areas:

| Tab | What you use it for |
| --- | --- |
| **Map** | Choose a mission, inspect coverage, follow your position, and request manual tests. |
| **Chat** | Send and receive short Meshtastic messages through the connected radio on an allowed channel. |
| **Activity** | Inspect GPS, radio activity, uploads, TX/RX evidence, and Watcher matching. |
| **Trips** | Review saved wardrives and selected coverage, and manage trip sharing. |
| **Radio** | Connect, enroll, recover, or disconnect your radio and control Offline Mode. |
| **Settings** | Configure driving behavior, appearance, profile/data options, updates, and support. |

Both platforms support Bluetooth and TCP radio connections; Android also supports USB serial radios. Follow the [Radio workflow](https://help.freqmapper.net/using-the-mobile-app/#radio) for transport-specific setup and permissions.

The iPhone release also includes an **Apple Watch companion** for starting, monitoring, and stopping a mapping trip through the paired iPhone. See the [iPhone release history](https://help.freqmapper.net/iphone-release-history/) for availability.

The [app workflow guide](https://help.freqmapper.net/using-the-mobile-app/) and [settings reference](https://help.freqmapper.net/mobile-app-settings/) explain the controls, map appearance, test pacing, ignored RX nodes, local data, offline recovery, and support options.

## Profiles, trips, sharing, and leaderboards

### Your account and linked phones

A website account is optional for basic use. Linking the app to a profile brings eligible uploaded activity from your linked phones and radios together, makes personal history available, and supports enrollment recovery after a reinstall or phone change.

Sign in at [My profile](https://freqmapper.net/profile) using a supported provider, then explicitly link the mobile app. Website sign-in and mobile linking are separate actions.

Your profile includes:

- **Overview:** personal coverage and activity totals.
- **Mapping pings:** individual tests, including standalone manual spot tests and available Watcher receipts.
- **Wardrive sessions:** uploaded trips, evidence, and optional sharing controls.
- **Linked apps & radios:** pair, name, find, and unlink installations.
- **Leaderboard:** review contributions and choose your public display preference.
- **Sign-in & security:** manage sign-in methods and account deletion.
- **Regional access:** open areas where you have an assigned role.

Link the app before uninstalling or changing phones, and finish pending uploads first. A profile does not serve as a backup of every phone-local setting or unsent record. Read [Profile and account settings](https://help.freqmapper.net/profile-settings/).

### Optional trip sharing

You can explicitly create a revocable link for a finished trip. It shows the selected trip's summary and eligible coverage cells. It does not publish the saved GPS route, exact individual TX/RX samples, radio identity, or private account details. Stop sharing to revoke the link.

The shared public map still contains the community's privacy-filtered aggregate coverage; Silent Recon contributions can appear there too. Receive-only does not mean the resulting aggregate coverage stays private.

### How contributions are counted

| Board | What it recognizes |
| --- | --- |
| **Active mappers** | Independently verified tests from the past seven days. |
| **Verified coverage leaders** | All eligible Watcher-verified tests in the selected area. |
| **Trailblazers** | First verified contributions in distinct 300 m overview cells. |
| **Watcher reach** | Different approved Watchers that received a mapper's tests. |
| **RX explorers** | Distinct 300 m areas with accepted receive evidence, once per mapper and area. |

Repeated RX packets can increase samples without adding another distinct-area point. A verified standalone manual test can earn eligible TX contribution credit without adding a wardrive session.

You can use an anonymous **Mapper code** or opt in to a chosen public driver name. Linking accounts does not automatically publish your sign-in identity as your leaderboard name.

Explore the [leaderboards](https://freqmapper.net/leaderboard) and read [how contribution totals work](https://help.freqmapper.net/leaderboards/).

## Regions, Watchers, and local mesh teams

### What is a region?

A region gives a local mesh community a name, boundary, public map, mapping policy, approved Watchers, and responsible stewards. **Region Groups** bring related regions together into a shared view while keeping their individual policies and evidence organized.

Use the global map to discover areas, then open a regional or group address. The [Freq51 map](https://freq51.freqmapper.net/) is one example. Read the [region guide index](https://help.freqmapper.net/region-guides/) and [Region Groups guide](https://help.freqmapper.net/multi-regions/).

### If your area is missing

Join [FreqMapper Discord](https://discord.gg/mccXD4qvgD) and explain your local mesh, approximate area, and who can help coordinate it. Setup is a reviewed community process and is not instant self-service.

A typical region needs:

1. A sensible proposed name and boundary.
2. A local contact or regional steward.
3. A working, locally operated receiving gateway and authorized MQTT source.
4. At least one approved Watcher providing real receipts for verified TX; two or more are strongly recommended.
5. An agreed mapping policy, radio compatibility, and a successful end-to-end test.

Your local team operates and maintains its radios, gateways, broker, and internet connection. FreqMapper integrates an authorized source; it does not supply that infrastructure. Mappers do not each need to run a Watcher or broker.

Start with [How FreqMapper works for mesh administrators](https://help.freqmapper.net/how-freqmapper-works/), [Start a region](https://help.freqmapper.net/start-a-region/), and [Help grow the map](https://help.freqmapper.net/help-grow-the-map/).

### Connecting an existing Watcher

A Watcher needs a stable gateway identity, actual RF receipts, an authorized MQTT path, and approval in the correct region. The gateway must be able to receive the mapping configuration used for the tests it will verify.

FreqMapper's connections to regional MQTT sources are **read-only**. They do not publish back to those brokers or send internet traffic onto RF. Active Patrol tests originate from the mapper's locally connected radio under regional policy.

Regional administrators manage their assigned areas; moderators have read-only review access. Signing in or holding an ordinary Discord role does not automatically grant FreqMapper regional access. Authorized operators can use the [regional administration reference](https://help.freqmapper.net/regional-administration/).

## Discord and other integrations

### FreqMapper in Discord

The [FreqMapper Wardriving Discord](https://discord.gg/mccXD4qvgD) is the community place for setup questions, enrollment help, and discussing new regions.

Where the bot is enabled, you can:

- Mention **@FreqMapper** with a Help question and follow its linked documentation.
- Use **/help**, **/status**, **/region info**, and **/leaderboard** for supported public information.
- Use **/mystats** for your linked personal contribution summary, or **/stats** to look up a public Mapper code.
- Use confirmed bug/feature reporting when the server enables those commands.
- Follow regional or group progress reports where the destination is configured.

Personal commands require the relevant linking steps. Command availability and permissions depend on the server and feature. The bot does not bridge Discord messages onto MQTT or RF.

Read the [Discord guide](https://help.freqmapper.net/discord/) for commands, linking, report follow-ups, and privacy boundaries.

### Partner applications

Approved applications can use read-only coverage feeds that explicitly distinguish **verified TX** from **passive RX**. The combined feed and compatible separate feeds are documented in the [partner coverage API guide](https://help.freqmapper.net/verified-coverage-api/). Integration approval and server-side credentials are separate from ordinary app enrollment.

These are privacy-limited integrations; they do not grant access to private trip routes, message contents, sign-in information, or Watcher identities. See the [integration overview](https://help.freqmapper.net/integrations/).

**MeshWars** describes using FreqMapper coverage for its Meshtastic board. MeshWars registration and FreqMapper radio enrollment are separate. Check its [documentation](https://meshwars.com/docs) and [Join page](https://meshwars.com/join) for current Meshtastic availability and rules. Use FreqMapper's own installation links above for the current app distribution.

## Privacy and control over your data

A trip you start can record a precise route and limited radio evidence for your personal history and verification. The **public map** receives privacy-filtered coverage aggregates rather than your precise trip route or individual RX records.

Other useful distinctions:

- Chat text stays on the phone under the documented local retention policy and is not uploaded as FreqMapper chat history. Radio transmissions still pass through the Meshtastic network.
- Public leaderboard names are optional; anonymous Mapper codes are available.
- Trip sharing is an explicit, revocable action.
- Support forms let you choose a public sanitized summary or a private report.
- Private routes and uploaded personal records are still data held by the service; public-map filtering does not mean nothing is collected.
- Unlinking a phone, clearing local history, uninstalling the app, and deleting server-side data are different actions.
- Account or unlinked-app deletion removes the covered personal records. De-identified community coverage can remain.

Read the [Privacy Policy](https://help.freqmapper.net/privacy/), [account-deletion guide](https://help.freqmapper.net/account-deletion/), and [Terms of Service](https://help.freqmapper.net/terms/) for the complete collection, retention, deletion, and service rules.

The map is not a guarantee of communication or an emergency communications service. Operate safely, respect local rules and channel practices, and use conservative mapping rates.

## Support, feedback, and contributing

### Get help

- Start with [Troubleshooting](https://help.freqmapper.net/troubleshooting/) and the [FAQ](https://help.freqmapper.net/frequently-asked-questions/).
- Ask setup and community questions in [FreqMapper Discord](https://discord.gg/mccXD4qvgD).
- For private support, account, privacy, or deletion questions, use the [Support guide](https://help.freqmapper.net/support/) or email [support@freqmapper.net](mailto:support@freqmapper.net).

### Report a bug or request a feature

[Search existing issues](https://github.com/Littleaton/FreqMapper-Feedback/issues) first, then [choose a report form](https://github.com/Littleaton/FreqMapper-Feedback/issues/new/choose).

For a bug, include the steps you took, what you expected, what happened instead, exact app version/build, phone and OS or browser, relevant radio model/firmware, approximate time, and general region. Sanitized screenshots can help.

For a feature, explain the mapping or radio problem you want to solve, who it affects, and any proposed approach.

You can also open **Settings → Help & about → Report a bug / Request a feature** in the app. Choose **Public summary** when a sanitized description may be published, or **Private report** for private-only support. The [Support guide](https://help.freqmapper.net/support/) explains replies and support activity.

**Direct GitHub issues and comments are public.** Never post enrollment codes, channel keys or QR codes, passwords, tokens, MQTT credentials, private messages, Bluetooth addresses, exact home/private locations, or unreviewed diagnostic files. Read [Privacy and reporting](PRIVACY_AND_REPORTING.md) before sharing attachments.

### Follow progress or help out

- Read and contribute to [open feedback discussions](https://github.com/Littleaton/FreqMapper-Feedback/issues).
- Check [closed issues](https://github.com/Littleaton/FreqMapper-Feedback/issues?q=is%3Aissue%20is%3Aclosed) for prior reports and decisions.
- Follow [product release notes](https://help.freqmapper.net/releases/) and [mobile release histories](https://help.freqmapper.net/app-release-history/) to see what has actually shipped.
- Map carefully, retest useful locations, suggest documentation corrections, or help your regional team maintain a reliable evidence source.
- Read [Contributing](https://help.freqmapper.net/contributing/) and [Help grow the map](https://help.freqmapper.net/help-grow-the-map/) to choose a useful next step.

An issue being closed does not by itself mean a fix is available in your installed app. A feature discussion is not a release commitment.

## Complete public guide directory

The Help site is the detailed reference. These links cover its public navigation; the release indexes lead to individual version notes and historical entries.

### First installation and first trip

| Guide | What you will find |
| --- | --- |
| [Help home](https://help.freqmapper.net/) | Overview and the main learning paths. |
| [Getting started](https://help.freqmapper.net/getting-started/) | Installation, prerequisites, enrollment, and the first-use sequence. |
| [Recommended hardware](https://help.freqmapper.net/recommended-hardware/) | Radios, frequency bands, antennas, power, and accessories. |
| [Enroll a mapping radio](https://help.freqmapper.net/join-a-mapping-region/) | Codes, connected-radio enrollment, and recovery expectations. |
| [Set up the app](https://help.freqmapper.net/set-up-the-app/) | Phone permissions, radio preparation, profile linking, and readiness. |
| [Your first mapping trip](https://help.freqmapper.net/first-mapping-trip/) | Missions, manual tests, offline preparation, evidence, and finishing. |

### Mobile app and map

| Guide | What you will find |
| --- | --- |
| [Using the mobile app](https://help.freqmapper.net/using-the-mobile-app/) | Map, Chat, Activity, Trips, Radio, and Settings. |
| [Mobile app settings](https://help.freqmapper.net/mobile-app-settings/) | Driving, startup, appearance, data, advanced options, and support. |
| [Map guide](https://help.freqmapper.net/map-guide/) | A starting explanation of coverage and map use. |
| [Public map controls and details](https://help.freqmapper.net/using-the-public-map/) | Regions, layers, cells, Watchers, and navigation. |
| [Complete map legend](https://help.freqmapper.net/map-legend/) | Evidence colors, outlines, markers, priority, and accessibility cues. |
| [Received here and passive RX](https://help.freqmapper.net/received-here/) | What was heard, where reception happened, and what becomes public. |
| [Leaderboards and contribution totals](https://help.freqmapper.net/leaderboards/) | TX contributions, Trailblazers, Watcher reach, RX points, and names. |

### Profile, privacy, and account

| Guide | What you will find |
| --- | --- |
| [Website profile and account](https://help.freqmapper.net/profile-settings/) | Linked apps/radios, personal history, sharing, names, and sign-in. |
| [Delete your account and data](https://help.freqmapper.net/account-deletion/) | Linked-account and unlinked-app deletion. |
| [Privacy Policy](https://help.freqmapper.net/privacy/) | Collection, public/private boundaries, retention, and removal. |
| [Terms of Service](https://help.freqmapper.net/terms/) | Acceptable use, responsibilities, and service limitations. |

### Regional communities and growing the map

| Guide | What you will find |
| --- | --- |
| [Region guide index](https://help.freqmapper.net/region-guides/) | Where regional organizers should begin. |
| [How FreqMapper works](https://help.freqmapper.net/how-freqmapper-works/) | Radio requirements, evidence flow, Watchers, and local responsibilities. |
| [Start a FreqMapper region](https://help.freqmapper.net/start-a-region/) | Proposing an area, infrastructure readiness, review, and activation. |
| [Regional administration](https://help.freqmapper.net/regional-administration/) | The reference for authorized regional operators. |
| [Region Groups](https://help.freqmapper.net/multi-regions/) | Shared regional views and inherited regional responsibilities. |
| [Contributing](https://help.freqmapper.net/contributing/) | Ways to take part. |
| [Help grow the map](https://help.freqmapper.net/help-grow-the-map/) | Mapping, existing feeders, and supporting your local team. |

### Integrations, questions, and support

| Guide | What you will find |
| --- | --- |
| [Integration overview](https://help.freqmapper.net/integrations/) | Supported user-facing integration paths. |
| [Discord bot](https://help.freqmapper.net/discord/) | Help answers, status, personal stats, regional information, and reports. |
| [Partner coverage API](https://help.freqmapper.net/verified-coverage-api/) | Approved read-only TX/RX feeds and their contracts. |
| [Support](https://help.freqmapper.net/support/) | Public/private reports, replies, account requests, and contact. |
| [Troubleshooting](https://help.freqmapper.net/troubleshooting/) | Radio connections, setup, Watchers, uploads, and recovery. |
| [Frequently asked questions](https://help.freqmapper.net/frequently-asked-questions/) | Short answers to common questions. |
| [Glossary](https://help.freqmapper.net/glossary/) | Plain definitions of FreqMapper and radio terms. |
| [Safe public reporting](PRIVACY_AND_REPORTING.md) | What belongs in this tracker and what must stay private. |

### Releases and updates

| Release page | What you will find |
| --- | --- |
| [All product releases](https://help.freqmapper.net/releases/) | The product release-note index and links to individual releases. |
| [Web changes](https://help.freqmapper.net/releases/web/) | Public website and map release notes. |
| [API and integrations](https://help.freqmapper.net/releases/api-integrations/) | Integration-facing release notes. |
| [Help site](https://help.freqmapper.net/releases/help/) | Documentation release notes. |
| [Discord](https://help.freqmapper.net/releases/discord/) | Bot release notes. |
| [Mobile apps](https://help.freqmapper.net/releases/mobile/) | Mobile changes within product releases. |
| [Infrastructure](https://help.freqmapper.net/releases/infrastructure/) | The public infrastructure release-note category. |
| [Mobile apps and updates](https://help.freqmapper.net/app-release-history/) | Documented app-store and tester releases and installation paths. |
| [Android release history](https://help.freqmapper.net/android-release-history/) | Android versions, builds, changes, and tester checks. |
| [Android OTA notes](https://help.freqmapper.net/android-ota-notes/) | Historical/private-installer release notes and update guidance. |
| [iPhone release history](https://help.freqmapper.net/iphone-release-history/) | App Store and external TestFlight releases. |

## About the project and this repository

This repository is for **public feedback and community discussion**. Application source code, deployment configuration, credentials, and private support evidence are maintained separately.

You can use the website, install the apps, contribute measurements, suggest improvements, and help a region without access to the application source.

Explore [FreqMapper](https://freqmapper.net/), read the [Help site](https://help.freqmapper.net/), or join [FreqMapper Discord](https://discord.gg/mccXD4qvgD) to get involved.

> I built FreqMapper with help from AI. It's closed source and only available as a free service I host for the Meshtastic community.
