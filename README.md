# ros2_notes
Some notes for my ROS2 voyage of discovery

## Cheat Sheet Reference

https://www.theroboticsspace.com/assets/article3/ros2_humble_cheat_sheet2.pdf


## Images

Below will broadcast a USB camera image onto topic /charlie/image
```
ros2 run image_tools cam2image --ros-args -r /image:=/charlie/image
```

If you try to subscribe across machines using raw images, you may get very poor performance. I suggest compressing:
You can compress this with:
```
ros2 run image_transport republish --ros-args -p in_transport:=raw -p out_transport:=compressed -r in:=/charlie/image -r out/compressed:=/charlie/compressed
```

And decompress with:
```
ros2 run image_transport republish --ros-args -p in_transport:=compressed -p out_transport:=raw -r /in/compressed:=/charlie/compressed -r /out:=/server/image
```

You can publish images that are being streamed over http. I have installed ipCam 1.2.2 SKJM installed on iPhone (from the Apple App Store)
```
ros2 run image_publisher image_publisher_node http://192.168.1.213/video.mjpg --ros-args -r /image_raw:=/ipad/image
```

Questions:
Can we pull images over USB in compressed format and send directly over network to save robot compute/latency?

