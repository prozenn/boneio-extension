# Bistable Channel

- Handles lighting circuits controlled by bistable relays and reads the real state from the second contact.
- Provides a `binary light`, `template output`, and `binary sensor` that keep Home Assistant in sync with the physical relay.

## Requirements

- Physical output `out_<pin>` defined in the main ESPHome configuration (for example a `gpio` that drives the relay coil).
- A configured `pcf8574` expander that exposes the feedback contact of the relay.

## Substitutions

| Key                   | Required | Default      | Description                                  |
|-----------------------|----------|--------------|----------------------------------------------|
| `bistable_name`       | no       | `"Światło"`  | Display name of the light entity.            |
| `bistable_output_pin` | yes      | —            | Pin number used to form IDs like `out_<pin>`.|
| `bistable_input_pcf`  | yes      | —            | ID of the `pcf8574` component that reads feedback. |
| `bistable_input_pin`  | yes      | —            | PCF pin connected to the feedback contact.   |
| `bistable_pulse`      | no       | `"200ms"`    | Pulse length sent to the relay coil.         |

From the pin number the module derives the IDs: `out_<pin>`, `out_<pin>_tpl`, `light_<pin>`, `input_<pin>`.

## Example (`vars`)

```yaml
packages:
  bistable_channel_17:
    url: https://github.com/prozenn/boneio-extension
    ref: v0.0.8
    files:
      - path: bistable_channel.yaml
        vars:
          bistable_name: "Test light"
          bistable_output_pin: "17"
          bistable_input_pcf: "pcf_inputs_15to28"
          bistable_input_pin: "4"
          # bistable_pulse: "200ms"
```

Ensure the main configuration defines `out_17` (or the pin you select) and that the related `pcf8574` is present so the virtual light always reflects the real relay state.
