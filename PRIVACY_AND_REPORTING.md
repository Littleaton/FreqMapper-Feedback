# Privacy and reporting

FreqMapper community reports should help reproduce a problem without exposing people, radios, or a mesh's private configuration.

## Safe to include

- App version, Android/iPhone model, operating-system version, and browser
- General region/IATA code when relevant
- A short, sanitized error message or crash report
- Screenshots with sensitive information removed
- Radio model and firmware version

## Never include

- Meshtastic channel PSKs, channel URLs, or provisioning QR codes
- API keys, passwords, bearer tokens, MQTT credentials, or server addresses intended to stay private
- Private messages or contact keys
- Exact home/private coordinates, personal addresses, or another person's location
- Logs that contain any of the above

## Before attaching a log or screenshot

1. Remove credentials, PSKs, and tokens.
2. Blur or crop exact private locations and personal identifiers.
3. Keep only the portion needed to explain the problem.

If an issue needs sensitive diagnostic details, do not post them publicly. Wait for a maintainer to provide a safe private contact path.