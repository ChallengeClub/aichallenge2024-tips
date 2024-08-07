# 20240717


## 障害物情報

/aichallenge/objects　トピックで配信されていました。
dataの中に、x, y, z, radiusを1つの障害物として格納されているようです。

```
ubuntu@ubuntu-desktop:~$ ros2 topic echo /aichallenge/objects
layout:
  dim: []
  data_offset: 0
data:
- 89617.6015625
- 43155.015625
- -29.500001907348633
- 1.25
- 89623.84375
- 43165.8671875
- -29.500001907348633
- 1.25
- 89630.875
- 43172.14453125
- -29.30000114440918
- 1.25
- 89658.1640625
- 43190.28515625
- -29.000001907348633
- 1.25
- 89651.359375
- 43171.8046875
- -29.10000228881836
- 1.25
- 89660.0
- 43157.79296875
- -29.30000114440918
- 1.25
- 89671.875
- 43149.0390625
- -29.30000114440918
- 1.25
- 89656.453125
- 43122.3203125
- -29.500001907348633
- 1.25
---
```

トピックの型を調査しました。[2024/8/7追記]
```
ubuntu@ubuntu-desktop:~$ ros2 topic info /aichallenge/objects -v
Type: std_msgs/msg/Float64MultiArray

Publisher count: 1

Node name: AWSIM
Node namespace: /
Topic type: std_msgs/msg/Float64MultiArray
Endpoint type: PUBLISHER
GID: 01.10.db.13.37.87.4b.5d.f9.b7.30.58.00.00.07.03.00.00.00.00.00.00.00.00
QoS profile:
  Reliability: RELIABLE
  History (Depth): KEEP_LAST (1)
  Durability: VOLATILE
  Lifespan: Infinite
  Deadline: Infinite
  Liveliness: AUTOMATIC
  Liveliness lease duration: Infinite

Subscription count: 3

Node name: object_marker
Node namespace: /
Topic type: std_msgs/msg/Float64MultiArray
Endpoint type: SUBSCRIPTION
GID: 01.10.4e.cc.bf.51.b6.e3.1e.36.64.4b.00.00.15.04.00.00.00.00.00.00.00.00
QoS profile:
  Reliability: RELIABLE
  History (Depth): KEEP_LAST (1)
  Durability: VOLATILE
  Lifespan: Infinite
  Deadline: Infinite
  Liveliness: AUTOMATIC
  Liveliness lease duration: Infinite

Node name: object_marker
Node namespace: /
Topic type: std_msgs/msg/Float64MultiArray
Endpoint type: SUBSCRIPTION
GID: 01.10.90.08.e4.5c.34.6a.9a.39.2e.18.00.00.15.04.00.00.00.00.00.00.00.00
QoS profile:
  Reliability: RELIABLE
  History (Depth): KEEP_LAST (1)
  Durability: VOLATILE
  Lifespan: Infinite
  Deadline: Infinite
  Liveliness: AUTOMATIC
  Liveliness lease duration: Infinite

Node name: rosbag2_recorder
Node namespace: /
Topic type: std_msgs/msg/Float64MultiArray
Endpoint type: SUBSCRIPTION
GID: 01.10.de.50.2e.1f.cd.7c.2c.62.b4.44.00.00.32.04.00.00.00.00.00.00.00.00
QoS profile:
  Reliability: RELIABLE
  History (Depth): KEEP_LAST (10)
  Durability: VOLATILE
  Lifespan: Infinite
  Deadline: Infinite
  Liveliness: AUTOMATIC
  Liveliness lease duration: Infinite

```


(参考)

```
ubuntu@ubuntu-desktop:~$ ros2 topic echo /aichallenge/objects_marker 
markers:
- header:
    stamp:
      sec: 69
      nanosec: 483336957
    frame_id: map
  ns: ''
  id: 0
  type: 3
  action: 0
  pose:
    position:
      x: 89622.9453125
      y: 43146.453125
      z: -29.500001907348633
    orientation:
      x: 0.0
      y: 0.0
      z: 0.0
      w: 1.0
  scale:
    x: 2.5
    y: 2.5
    z: 1.0
  color:
    r: 1.0
    g: 0.0
    b: 1.0
    a: 1.0
  lifetime:
    sec: 0
    nanosec: 0
  frame_locked: false
  points: []
  colors: []
  texture_resource: ''
  texture:
    header:
      stamp:
        sec: 0
        nanosec: 0
      frame_id: ''
    format: ''
    data: []
  uv_coordinates: []
  text: ''
  mesh_resource: ''
  mesh_file:
    filename: ''
    data: []
  mesh_use_embedded_materials: false
- header:
    stamp:
      sec: 69
      nanosec: 483336957
    frame_id: map
  ns: ''
  id: 1
  type: 3
  action: 0
  pose:
    position:
      x: 89630.453125
      y: 43148.140625
      z: -29.500001907348633
    orientation:
      x: 0.0
      y: 0.0
      z: 0.0
      w: 1.0
  scale:
    x: 2.5
    y: 2.5
    z: 1.0
  color:
    r: 1.0
    g: 0.0
    b: 1.0
    a: 1.0
  lifetime:
    sec: 0
    nanosec: 0
  frame_locked: false
  points: []
  colors: []
  texture_resource: ''
  texture:
    header:
      stamp:
        sec: 0
        nanosec: 0
      frame_id: ''
    format: ''
    data: []
  uv_coordinates: []
  text: ''
  mesh_resource: ''
  mesh_file:
    filename: ''
    data: []
  mesh_use_embedded_materials: false
- header:
    stamp:
      sec: 69
      nanosec: 483336957
    frame_id: map
  ns: ''
  id: 2
  type: 3
  action: 0
  pose:
    position:
      x: 89632.265625
      y: 43164.55859375
      z: -29.30000114440918
    orientation:
      x: 0.0
      y: 0.0
      z: 0.0
      w: 1.0
  scale:
    x: 2.5
    y: 2.5
    z: 1.0
  color:
    r: 1.0
    g: 0.0
    b: 1.0
    a: 1.0
  lifetime:
    sec: 0
    nanosec: 0
  frame_locked: false
  points: []
  colors: []
  texture_resource: ''
  texture:
    header:
      stamp:
        sec: 0
        nanosec: 0
      frame_id: ''
    format: ''
    data: []
  uv_coordinates: []
  text: ''
  mesh_resource: ''
  mesh_file:
    filename: ''
    data: []
  mesh_use_embedded_materials: false
- header:
    stamp:
      sec: 69
      nanosec: 483336957
    frame_id: map
  ns: ''
  id: 3
  type: 3
  action: 0
  pose:
    position:
      x: 89648.328125
      y: 43184.3125
      z: -29.000001907348633
    orientation:
      x: 0.0
      y: 0.0
      z: 0.0
      w: 1.0
  scale:
    x: 2.5
    y: 2.5
    z: 1.0
  color:
    r: 1.0
    g: 0.0
    b: 1.0
    a: 1.0
  lifetime:
    sec: 0
    nanosec: 0
  frame_locked: false
  points: []
  colors: []
  texture_resource: ''
  texture:
    header:
      stamp:
        sec: 0
        nanosec: 0
      frame_id: ''
    format: ''
    data: []
  uv_coordinates: []
  text: ''
  mesh_resource: ''
  mesh_file:
    filename: ''
    data: []
  mesh_use_embedded_materials: false
```



## 自己位置
自己位置は、/sensing/gnss/pose トピックに出ているようです。

```
ubuntu@ubuntu-desktop:~$ ros2 topic echo /sensing/gnss/pose          
header:
  stamp:
    sec: 319
    nanosec: 983350021
  frame_id: map
pose:
  position:
    x: 89656.8984375
    y: 43172.8046875
    z: -29.06036376953125
  orientation:
    x: 0.0
    y: 0.0
    z: 0.0
    w: 0.0
---

```

トピックの型を調査しました。[2024/8/7追記]
```
ubuntu@ubuntu-desktop:~$ ros2 topic info /sensing/gnss/pose -v
Type: geometry_msgs/msg/PoseStamped

Publisher count: 1

Node name: AWSIM
Node namespace: /
Topic type: geometry_msgs/msg/PoseStamped
Endpoint type: PUBLISHER
GID: 01.10.db.13.37.87.4b.5d.f9.b7.30.58.00.00.0f.03.00.00.00.00.00.00.00.00
QoS profile:
  Reliability: RELIABLE
  History (Depth): KEEP_LAST (1)
  Durability: VOLATILE
  Lifespan: Infinite
  Deadline: Infinite
  Liveliness: AUTOMATIC
  Liveliness lease duration: Infinite

Subscription count: 1

Node name: rosbag2_recorder
Node namespace: /
Topic type: geometry_msgs/msg/PoseStamped
Endpoint type: SUBSCRIPTION
GID: 01.10.de.50.2e.1f.cd.7c.2c.62.b4.44.00.00.4f.04.00.00.00.00.00.00.00.00
QoS profile:
  Reliability: RELIABLE
  History (Depth): KEEP_LAST (10)
  Durability: VOLATILE
  Lifespan: Infinite
  Deadline: Infinite
  Liveliness: AUTOMATIC
  Liveliness lease duration: Infinite

```