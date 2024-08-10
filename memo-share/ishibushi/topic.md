# トピック仕様
[仕様](https://automotiveaichallenge.github.io/aichallenge-documentation-2024/specifications/interface.html)に記載されていること ＋ 確認したことをメモとして記載していく

# ピットインエリアのトピック
## 確認方法
```
ros2 topic echo /aichallenge/pitstop/area
```
## publishされるタイミング
スタート時に１度のみ。変更されることはない
## タイプ
```
std_msgs/msg/Float64MultiArray
```

# ゴールのトピック
## 確認方法
```
ros2 topic echo /planning/mission_planning/goal
```
## publishされるタイミング
コース半周ごとに飛ばされる。目的地との距離がしきい値以下になると到着とみなす。
しきい値は goal_pose_setter のconfig で設定可能
## タイプ
```
geometry_msgs/msg/PoseStamped
```

# コンディションのトピック
## 確認方法
```
ros2 topic echo  /aichallenge/pitstop/condition
```
## publishされるタイミング
10hz? 程度で常にと飛ばされている。

## タイプ
```
std_msgs/msg/Int32
```
## ペナルティ
- 1週目は何もしなくても240まで上昇する。おそらく8つの障害物ポイントを通過するだけで 30 は増加する仕様。
- 1000 以上になると制限速度がかかる。 [ルール](https://automotiveaichallenge.github.io/aichallenge-documentation-2024/information/rules.html)参照。

# 障害物トピック
## 確認方法
```
ros2 topic echo /aichallenge/objects
```
## タイプ
```
std_msgs/msg/Float64MultiArray
```
- 障害物の座標と半径が格納される配列。
- X, Y , Z ,半径の順に格納される。
  
## publishされるタイミング
10hz? 程度で常にと飛ばされている。

# 車両の舵角のトピック
## 確認方法
```
ros2 topic echo /vehicle/status/steering_status
```

## タイプ
```
autoware_auto_vehicle_msgs/msg/SteeringReport
```


## publishされるタイミング
```
30?hz 程度で常にと飛ばされている。
```


# 車両の速度のトピック
## 確認方法
```
ros2 topic echo  /vehicle/status/velocity_status
```

## タイプ
```
autoware_auto_vehicle_msgs/msg/VelocityReport
```


## publishされるタイミング
```
30?hz 程度で常にと飛ばされている。
```

# 制御コマンド
## 確認方法
```
ros2 topic echo  /control/command/control_cmd
```
## タイプ
```
autoware_auto_control_msgs/msg/AckermannControlCommand
```
## publishされるタイミング
```
35?hz 程度で常にと飛ばされている。
```