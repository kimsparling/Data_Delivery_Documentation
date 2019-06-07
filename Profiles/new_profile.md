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

* Create your JSON payload. 
<<<<<<< HEAD
 <details>
    <summary> Example: </summary>
    
=======
    <details>
        <summary> Example:</summary>
      Test
    </details>
>>>>>>> 675a02dfa08922c03fadcd4a5416b4f7510ad5e9
```json
{
"name": "gen5_gulfstream2019_3ir_slow",
"title" : "Gulf Stream 2019 IR Thermo High Resolution Data",
"description": "Custom profile used for high res data delivery for the Gulf Stream 2019 Mission.",
  "created_by": 425,
"body":{
"variables" : [
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
},
{
"node": "sky_ir_thermo",
"topic": "raw",
"field": "temperature"
},
{
  "name": "AMBIENT_TEMP_IR_SKY",
  "long_name": "Sky ambient temperature",
"node": "sky_ir_thermo",
"topic": "raw",
"field": "ambient_temperature"
},
{
    "name": "RADIANCE_IR_SKY",
  "long_name": "Sky radiance",
"node": "sky_ir_thermo",
"topic": "raw",
"field": "radiance"
},
{
  "name": "TEMP_IR_SKY",
  "long_name": "Sky temperature",
"node": "sea_ir_thermo",
"topic": "raw",
"field": "temperature"
},
{
  "name": "AMBIENT_TEMP_IR_SEA",
  "long_name": "Hull ambient temperature",
"node": "sea_ir_thermo",
"topic": "raw",
"field": "ambient_temperature"
},
{
    "name": "RADIANCE_IR_SEA",
  "long_name": "Hull radiance",
"node": "sea_ir_thermo",
"topic": "raw",
"field": "radiance"
},
{
  "name" : "TEMP_IR_WING",
  "long_name": "Wing Skin temperature",
"node": "ir_thermo",
"topic": "raw",
"field": "temperature"
},
{
  "name": "AMBIENT_TEMP_IR_WING",
  "long_name": "Wing ambient temperature",
"node": "ir_thermo",
"topic": "raw",
"field": "ambient_temperature"
},
{
      "name": "RADIANCE_IR_WING",
  "long_name": "Wing radiance",
"node": "ir_thermo",
"topic": "raw",
"field": "radiance"
},
{
"node": "bosun",
"field": "roll",
"topic": "data"
},
{
"node": "bosun",
"field": "pitch",
"topic": "data"
},
{
"node": "bosun",
"field": "yaw",
"topic": "data"
},
{
"node": "bosun",
"field": "wing_roll",
"topic": "data"
},
{
"node": "bosun",
"field": "wing_pitch",
"topic": "data"
},
{
"node": "bosun",
"field": "wing_yaw",
"topic": "data"
},
{
"name": "INS_HULL_VEL_E",
"node": "imu_hull",
"field": "ins_velocity_e",
"topic": "velocity",
"long_name": "INS hull velocity E"
},
{
"name": "INS_HULL_VEL_N",
"node": "imu_hull",
"field": "ins_velocity_n",
"topic": "velocity",
"long_name": "INS hull velocity N"
},
{
"name": "INS_HULL_VEL_U",
"node": "imu_hull",
"field": "ins_velocity_d",
"topic": "velocity",
"long_name": "INS hull velocity U",
"transformation": "*-1"
},
{
"name": "INS_HULL_QUAT_W",
"node": "imu_hull",
"field": "rot_quat_w",
"topic": "rot",
"long_name": "INS hull quaternion W"
},
{
"name": "INS_HULL_QUAT_X",
"node": "imu_hull",
"field": "rot_quat_x",
"topic": "rot",
"long_name": "INS hull quaternion X"
},
{
"name": "INS_HULL_QUAT_Y",
"node": "imu_hull",
"field": "rot_quat_y",
"topic": "rot",
"long_name": "INS hull quaternion Y"
},
{
"name": "INS_HULL_QUAT_Z",
"node": "imu_hull",
"field": "rot_quat_z",
"topic": "rot",
"long_name": "INS hull quaternion Z"
},
{
"name": "INS_WING_VEL_E",
"node": "imu_wing",
"field": "ins_velocity_e",
"topic": "velocity",
"long_name": "INS wing velocity E"
},
{
"name": "INS_WING_VEL_N",
"node": "imu_wing",
"field": "ins_velocity_n",
"topic": "velocity",
"long_name": "INS wing velocity N"
},
{
"name": "INS_WING_VEL_U",
"node": "imu_wing",
"field": "ins_velocity_d",
"topic": "velocity",
"long_name": "INS wing velocity U",
"transformation": "*-1"
},
{
"name": "INS_WING_QUAT_W",
"node": "imu_wing",
"field": "rot_quat_w",
"topic": "rot",
"long_name": "INS wing quaternion W"
},
{
"name": "INS_WING_QUAT_X",
"node": "imu_wing",
"field": "rot_quat_x",
"topic": "rot",
"long_name": "INS wing quaternion X"
},
{
"name": "INS_WING_QUAT_Y",
"node": "imu_wing",
"field": "rot_quat_y",
"topic": "rot",
"long_name": "INS wing quaternion Y"
},
{
"name": "INS_WING_QUAT_Z",
"node": "imu_wing",
"field": "rot_quat_z",
"topic": "rot",
"long_name": "INS wing quaternion Z"
}
]
}
}
```
</details>
