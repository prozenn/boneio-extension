# Binary Light

Provides a binary light that uses an existing `out_*` output and a PCF8574 input to toggle its state. The module automatically imports `pcf_configuration.yaml` so it can translate input numbers to the correct `pcf8574` expander and pin.

## Entities

- `light`: Binary light bound to the chosen output.
- `binary_sensor`: PCF8574-backed input that toggles the light on press.

## Substitutions

| Key                     | Required | Default            | Description                                      |
|-------------------------|----------|--------------------|--------------------------------------------------|
| `binary_light_output`   | yes      | —                  | Numeric channel used to build `out_<n>` and `light_<n>`. |
| `binary_light_input`    | yes      | —                  | Numeric input used to build `IN_<n>`/`in_<n>` and look up the PCF mapping. |
| `binary_light_name`     | no       | `"Light <n>"`      | Display name of the light entity.                |
| `binary_light_input_name` | no     | `"IN_<n>"`         | Display name of the binary sensor.               |

## Example (`vars`)

```yaml
packages:
  binary_light_17:
    url: https://github.com/prozenn/boneio-extension
    ref: v0.0.8
    files:
      - path: binary_light.yaml
        vars:
          binary_light_output: "17"
          binary_light_input: "17"
          binary_light_name: "Light 17"
          binary_light_input_name: "IN_17"
```

Ensure the output `out_17` and the referenced `pcf8574` component exist in the main configuration so the light stays synchronised with the physical input.
