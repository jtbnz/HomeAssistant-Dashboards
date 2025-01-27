
<img src="images\dashboard.png" alt="Example Dashboard" width="50%">


automation to start the rotation

```yaml
alias: Twinkly rotation
description: ""
triggers:
  - trigger: time_pattern
    minutes: /1
conditions:
  - condition: device
    type: is_on
    device_id: 80f95510144c5e9085cc785aa6425608
    entity_id: aa1c394e844a3ae038c396fffc3ae8e1
    domain: light
    enabled: false
  - condition: and
    conditions: a
      - condition: time
        after: "07:00:00"
        before: "23:00:00"
        weekday:
          - sun
          - mon
          - tue
          - wed
          - thu
          - fri
          - sat
actions:
  - action: light.turn_on
    data_template:
      entity_id: light.twinkly1
      effect: >
        {% set effects = state_attr('light.twinkly1', 'effect_list') %} {% set
        current_effect = state_attr('light.twinkly1', 'effect') %} {% set
        next_index = (effects.index(current_effect) + 1) % effects | length %}
        {{ effects[next_index] }}
mode: single
```