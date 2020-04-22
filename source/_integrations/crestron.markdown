---
title: Crestron
description: Instructions on how to communicate with a Crestron processor with Home Assistant.
ha_category:
  - Binary Sensor
  - Switch
ha_release: 0.101
ha_iot_class: Local Polling
ha_codeowners:
  - '@rzulian'
ha_domain: crestron
---

[Crestron](http://www.crestron.com/) is an American  company. They have several lines of home automation devices that manage light switches/dimmers, occupancy sensors, HVAC controls, etc. The `crestron` integration in Home Assistant is responsible for communicating   with a Crestron control processor using the Crestron-over-IP (CIP) protocol.

Familiarity with and access to Crestron's development tools, processes and terminology are required to configure the control processor in a way that allows this module to be used.

## Configuration

This module works by connecting to an "XPanel 2.0 Smart Graphics" symbol defined in a SIMPL Windows program. Once the control processor has been programmed accordingly, you can communicate with it using the API as described below.

``` yaml
# Example configuration.yaml entry
crestron:
  host: crestron_ip
  ipid: crestron_ipid
  port: 41794
```

{% configuration %}
host:
  description: The IP address of the Crestron processor.
  required: true
  type: string
ipid:
  description: The IPID of the XPanel symbol
  required: true
  type: integer
port:
  description: The port  
  required: false
  type: integer
  default: 41794
{% endconfiguration %}

<div class='note'>


</div>

``` yaml

binary_sensor:
  - platform: crestron
    name: btn_from_crestron
    digital_join_in_status: 41


switch:
  - platform: crestron
    name: cmd_to_crestron
    join: 34
    join_is_pulsed: True
```

## Keypad buttons


## Keypad LEDs


## Scene


## Occupancy Sensors


## Example Automations

``` yaml
- alias: "keypad button pressed notification"
  trigger:
    - platform: event
      event_type: lutron_event
      event_data:
        id: office_pico_on
        action: single
  action:
    - service: notify.telegram
      data:
        message: "pico just turned on!"
```

