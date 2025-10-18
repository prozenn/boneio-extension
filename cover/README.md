# Time-Based Cover

- Provides a `time_based` cover entity with open and close actions routed through existing `switch` components.
- Exposes two `binary_sensor` inputs that can trigger open/close/stop commands from physical buttons wired via PCF8574 expanders.

## Requirements

- Two `switch` components (for example `template`, `gpio`, or `output`-backed relays) that actually energize the cover motor in each direction.
- PCF8574 expanders mapped to the physical "open" and "close" buttons.
- A substitutions dictionary `pcf_inputs` that maps numeric identifiers (`"01"`, `"02"`, …) to `[pcf_id, pin]`, for example by including `pcf_configuration.yaml`.

## Substitutions

| Key                     | Required | Default | Description                                                         |
|-------------------------|----------|---------|---------------------------------------------------------------------|
| `cover_name`            | no       | `"Cover"` | Display name of the cover entity.                                  |
| `cover_output_pin`      | yes      | —       | Suffix used to build IDs such as `cover_<pin>`.                     |
| `cover_open_switch`     | yes      | —       | ID of the `switch` that energizes the motor in the open direction.  |
| `cover_close_switch`    | yes      | —       | ID of the `switch` that energizes the motor in the close direction. |
| `cover_open_duration`   | no       | `"10s"` | Motor run time while opening.                                       |
| `cover_close_duration`  | no       | `"10s"` | Motor run time while closing.                                       |

## Example (`vars`)

```yaml
substitutions: !include pcf_configuration.yaml

packages:
  cover_01:
    url: https://github.com/prozenn/boneio-extension
    ref: v0.0.8
    files:
      - path: cover/time_based_cover.yaml
        vars:
          cover_name: "Cover 01"
          cover_output_pin: "01"
          cover_open_switch: "cover_open_01_out01"
          cover_close_switch: "cover_close_01_out02"
          cover_open_duration: "10s"
          cover_close_duration: "10s"
```

Ensure that the referenced `switch` components, PCF8574 expanders, and the `pcf_inputs` substitution dictionary are declared in the main ESPHome configuration, and that the wiring prevents both motor directions from being energized simultaneously.
