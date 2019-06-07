# Creating a New Profile

You may need to create a new profile for any of the following reasons:
* There is a new mission
* A customer requested custom data
* A drone has both fast (20 Hz) and slow (1 Hz) collecting sensors

Use the steps below as a guideline for creating those new profiles.

* Check [Meta](https://meta.saildrone.com/drones?limit=500&offset=0&order_by=desc&sort_by=id) :
    * See what sensors are on the drone. This should have info about the sampling rate associated with the sensors.
    * Cross check the sensors with the available Nodes. This will give you a list of Node:Topic:Fields that can be in the profile.

*  Reference profiles that have already been made. A great starting point is [gen5_fast](https://exporter-controller.saildrone.com/v1/profiles/gen5_fast) and [gen5_slow](https://exporter-controller.saildrone.com/v1/profiles/gen5_slow). See also [profiles](profiles.md). Gather the relevant sensor N:T:F data and add new N:T:Fs that you found in the previous step.
*  Make sure that these two fields are at the top:
```json
        {
          "node": "gps",
          "field": "lat",
          "topic": "location",
          "coordinate": "latitude",
          "standard_name": "latitude"
        },
        {
          "node": "gps",
          "field": "lng",
          "topic": "location",
          "coordinate": "longitude",
          "standard_name": "longitude"
        }

```

* If [Meta](https://meta.saildrone.com/atoms) does not have a name and long_name associated with the N:T:F, you will likely want to manually add one. For example, at the time of writing, `ambient_temperature` does not have an associated name or long_name. These items must be added to the JSON snippet in order to show up in the netcdf:
```json
        {
          "name": "AMBIENT_TEMP_IR_SKY",
          "node": "sky_ir_thermo",
          "field": "ambient_temperature",
          "topic": "raw",
          "long_name": "Sky ambient temperature"
        }
```

* Name your profile according to standard naming practice: `[generation]_[mission]_[customization]_[sample rate]`
    * Example : `gen5_gulfstream2019_3ir_slow` means that :
        * we're using gen5 drones
        * the mission is gulfstream2019
        * someone requested 3 IR sensor data
        * the sensors sample at 1 Hz. 