# Camera-sounds add-on for Home Assistant
CeC
July 2024

# This is under development - not even a beta yet 

### ...nothing to see here...

---


Use the YAMNet sound model to characterize sound using  microphones on remote cameras 
It's not recording to keep anything, just taking 5s samples periodically and classifying
the sound, ideally to be able to detect people sounds, traffic sounds, storms, etc.
I was motivated by an interest in being able to detect that peeople are hanging out
even if they are outside of the camera's field of view.  Detecting a tornado 
warning siren migth not be a bad thing either.

This add-on has only been tested on Amcrest
cameras so it's far from proven.



0. This addon assumes you are running a MQTT broker already. This code
has (only) been tested with the open source
[Mosquitto broker](https://github.com/home-assistant/addons/tree/master/mosquitto) 
from the *Official add-ons* repository.

1. Create a file, *microphones.yaml* with specifics regarding your MQTT broker address,
MQTT username and password, and RTSP feeds. These will be the same feeds you use
in Frigate (if you use Frigate), which may have embedded credentials
(so treat this as a secrets file). If you want to report less frequently than
every 60s you can change the *stats_interval* value in this file.  This configuration
file will look something like below. Put this file into */config*.

```
mqtt:
  host: "x.x.x.x"
  port: 1883
  topic_prefix: "HA/sensor"
  client_id: "yamcam"
  user: "mymqttusernameforcamvol"
  password: "mymqttpasswordforcamvol"
  stats_interval: 30
cameras:
  doorfrontcam:
    ffmpeg:
      inputs:
      - path: "rtsp://user:password@x.x.x.x:554/cam/realmonitor?channel=1&subtype=1"
  frontyardcam:
    ffmpeg:
      inputs:
      - path: "rtsp://user:password@x.x.x.x:554/cam/realmonitor?channel=1&subtype=1"
```



