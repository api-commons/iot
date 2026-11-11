# IoT Devices

The common IoT vocabulary -- the devices in the field, the sensors on them, the telemetry they report, the commands sent back to them and the firmware updates that keep them current -- distilled from the APIs that already exist. Vehicles belong to the fleet context. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged IoT, Internet of Things, Industrial IoT, IIoT, Sensors, Smart Home, Device Management, Connected Devices in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| device | 69 | 62 | name 68%, type 55%, id 53% | devices 55, device 17, gateways 10, things 3 |
| telemetry | 18 | 14 | timestamp 50% | data 5, events 4, telemetry 3, timeseries 3 |
| device_command | 12 | 10 | command 60%, status 60% | commands 6, actions 3, jobs 2, rpc 2 |
| firmware_update | 11 | 8 | description 50% | firmware 6, ota 3, updates 2 |

Cohort: 195 providers with harvested OpenAPI, 69 crosswalks. Of the providers exposing a device: 46% create, 93% list, 75% fetch, 41% update, 46% delete. Generated 2026-11-10 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A device agrees on name, id and type across IoT clouds, smart-home platforms and industrial systems; firmware version and last-seen time are carried by too few to share.
- Telemetry agrees only on a timestamp: a reading is a value, a map of values, a fragment (Cumulocity) or a sample with every sensor in it, depending on the platform.
- A device command agrees on the command and its status -- the remote-procedure-call shape that IoT platforms share.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Things, gateways and endpoints beneath a device path are devices; vehicles are fleet's.
- Readings, measurements, samples and device events are telemetry.
- Device jobs (AWS IoT) and RPC calls are device commands; OTA jobs and firmware deployments are firmware updates (`/firmware-updates`).
- Sensors were measured and dropped (1 provider).
- Duplicates merged: three AWS IoT listings into AWS IoT Core.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
