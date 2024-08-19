# 📺 Roku Remote Card

[![GitHub Release][releases-shield]][releases]
[![License][license-shield]](LICENSE.md)
[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg?style=for-the-badge)](https://github.com/hacs/integration)

![Project Maintenance][maintenance-shield]
[![GitHub Activity][commits-shield]][commits]


[![Twitter][twitter]][twitter]
[![Github][github]][github]

Note: This repository has been modified for personal use. If you wish to use the original you may do so here: https://github.com/iantrich/roku-card


![example](example.png)

## Installation

# Version 1.1.0 and above require Home Assistant 0.110.0 or above

Use [HACS](https://hacs.xyz) or follow this [guide](https://github.com/thomasloven/hass-config/wiki/Lovelace-Plugins)

```yaml
resources:
  url: /local/roku-card.js
  type: module
```

## Options

| Name        | Type      | Requirement  | Description                                                                                            |
| ----------- | --------- | ------------ | ------------------------------------------------------------------------------------------------------ |
| type        | `string`  | **Required** | `custom:roku-card`                                                                                     |
| entity      | `string`  | **Required** | `media_player` entity of Roku device                                                                   |
| remote      | `string`  | **Optional** | `remote` entity of Roku device. Default assumed named like `entity`                                    |
| name        | `string`  | **Optional** | Card name                                                                                              |
| theme       | `string`  | **Optional** | Card theme                                                                                             |
| tv          | `boolean` | **Optional** | If `true` shows volume and power buttons. Default `false`                                              |
| power       | `map`     | **Optional** | Button configuration for power [See button options](#button-options)                                   |
| volume_up   | `map`     | **Optional** | Button configuration for volume_up [See button options](#button-options)                               |
| volume_down | `map`     | **Optional** | Button configuration for volume_down [See button options](#button-options)                             |
| volume_mute | `map`     | **Optional** | Button configuration for volume_mute [See button options](#button-options)                             |
| up          | `map`     | **Optional** | Button configuration for up [See button options](#button-options)                                      |
| down        | `map`     | **Optional** | Button configuration for down [See button options](#button-options)                                    |
| left        | `map`     | **Optional** | Button configuration for left [See button options](#button-options)                                    |
| right       | `map`     | **Optional** | Button configuration for right [See button options](#button-options)                                   |
| home        | `map`     | **Optional** | Button configuration for home [See button options](#button-options)                                    |
| info        | `map`     | **Optional** | Button configuration for info [See button options](#button-options)                                    |
| back        | `map`     | **Optional** | Button configuration for back [See button options](#button-options)                                    |
| select      | `map`     | **Optional** | Button configuration for select [See button options](#button-options)                                  |
| reverse     | `map`     | **Optional** | Button configuration for reverse [See button options](#button-options)                                 |
| play        | `map`     | **Optional** | Button configuration for play [See button options](#button-options)                                    |
| forward     | `map`     | **Optional** | Button configuration for forward [See button options](#button-options)                                 |
| apps        | `map`     | **Optional** | List of app shortcuts [See app options](#app-options)                                                  |
| haptic      | `string`  | **Optional** | `none`, `success`, `warning`, `failure`, `light`, `medium`, `heavy`, `selection`. Default is `success` |

## app Options

| Name              | Type     | Requirement  | Description                                                 |
| ----------------- | -------- | ------------ | ----------------------------------------------------------- |
| app               | `string` | **Optional** | Name of the source to launch as `tap_action`                |
| image             | `string` | **Optional** | Path to image to use for app                                |
| icon              | `string` | **Optional** | mdi icon to use instead of an image for app                 |
| tap_action        | `map`    | **Optional** | Tap action map [See action options](#action-options)        |
| hold_action       | `map`    | **Optional** | Hold action map [See action options](#action-options)       |
| double_tap_action | `map`    | **Optional** | Doulbe Tap action map [See action options](#action-options) |

## button Options

| Name              | Type      | Requirement  | Description                                                 |
| ----------------- | --------- | ------------ | ----------------------------------------------------------- |
| show              | `boolean` | **Optional** | Show/Hide button `true`                                     |
| tap_action        | `map`     | **Optional** | Tap action map [See action options](#action-options)        |
| hold_action       | `map`     | **Optional** | Hold action map [See action options](#action-options)       |
| double_tap_action | `map`     | **Optional** | Doulbe Tap action map [See action options](#action-options) |

## action Options

| Name              | Type     | Default  | Supported options                                                        | Description                                                                                               |
| ----------------- | -------- | -------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------- |
| `action`          | `string` | `toggle` | `more-info`, `toggle`, `call-service`, `none`, `navigate`, `url`         | Action to perform                                                                                         |
| `entity`          | `string` | none     | Any entity id                                                            | **Only valid for `action: more-info`** to override the entity on which you want to call `more-info`       |
| `navigation_path` | `string` | none     | Eg: `/lovelace/0/`                                                       | Path to navigate to (e.g. `/lovelace/0/`) when action defined as navigate                                 |
| `url_path`        | `string` | none     | Eg: `https://www.google.com`                                             | URL to open on click when action is `url`.                                                                |
| `service`         | `string` | none     | Any service                                                              | Service to call (e.g. `media_player.media_play_pause`) when `action` defined as `call-service`            |
| `service_data`    | `map`    | none     | Any service data                                                         | Service data to include (e.g. `entity_id: media_player.bedroom`) when `action` defined as `call-service`. |
| `haptic`          | `string` | none     | `success`, `warning`, `failure`, `light`, `medium`, `heavy`, `selection` | Haptic feedback for the [Beta IOS App](http://home-assistant.io/ios/beta)                                 |
| `repeat`          | `number` | none     | eg: `500`                                                                | How often to repeat the `hold_action` in milliseconds.                                                    |

## Usage

```yaml
type: custom:roku-card
entity: media_player.michaels_roku
tv: true
apps:
  - image: /local/icons/Icon-YouTube.png
    app: YouTube
    tap_action:
      action: call-service
      haptic: success
      service: media_player.select_source
      service_data:
        source: YouTube
        entity_id: media_player.michaels_roku
  - image: /local/icons/Icon-Twitch.png
    app: Stitch
    tap_action:
      action: call-service
      haptic: success
      service: media_player.select_source
      service_data:
        source: Stitch
        entity_id: media_player.michaels_roku
  - image: /local/icons/Icon-Floatplane.png
    app: Hydravion
    tap_action:
      action: call-service
      haptic: success
      service: media_player.select_source
      service_data:
        source: Hydravion
        entity_id: media_player.michaels_roku
  - image: /local/icons/Icon-AppleMusic.png
    app: Apple Music
    tap_action:
      action: call-service
      haptic: success
      service: media_player.select_source
      service_data:
        source: Apple Music
        entity_id: media_player.michaels_roku
volume_up:
  tap_action:
    action: call-service
    haptic: success
    service: remote.send_command
    service_data:
      entity_id: remote.michaels_roku
      command: volume_up
volume_down:
  tap_action:
    action: call-service
    haptic: success
    service: remote.send_command
    service_data:
      entity_id: remote.michaels_roku
      command: volume_down
volume_mute:
  tap_action:
    action: call-service
    haptic: success
    service: remote.send_command
    service_data:
      entity_id: remote.michaels_roku
      command: volume_mute
forward:
  show: false
reverse:
  show: false
play:
  show: false
power:
  show: false

```

[Troubleshooting](https://github.com/thomasloven/hass-config/wiki/Lovelace-Plugins)


[commits-shield]: https://img.shields.io/github/commit-activity/y/Narehood/roku-card.svg?style=for-the-badge
[commits]: https://github.com/Narehood/roku-card/commits/master
[forum-shield]: https://img.shields.io/badge/community-forum-brightgreen.svg?style=for-the-badge
[forum]: https://community.home-assistant.io/t/lovelace-roku-remote-card/91476
[license-shield]: https://img.shields.io/github/license/Narehood/roku-card.svg?style=for-the-badge
[releases-shield]: https://img.shields.io/github/release/Narehood/roku-card.svg?style=for-the-badge
[releases]: https://github.com/Narehood/roku-card/releases
[twitter]: https://img.shields.io/twitter/follow/michaelnarehood.svg?style=social
[github]: https://img.shields.io/github/followers/Narehood.svg?style=social
