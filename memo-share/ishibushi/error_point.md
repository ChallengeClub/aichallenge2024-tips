# 開始時にrviz の緑の線が表示されない。
## default_goal_pose.param.yaml
- yamlの値 goal_range などは小数点まできっちり書く。
- as_double() で読み込まれるので整数だとロードされない

# たまにrviz 動かない
 - デバッグ中にrviz が立ち上がらない現象がたまにある。docker を落とすと解決する

# コンパイル時
## BOOST_HEADER_DEPRECATED("<boost/core/no_exceptions_support.hpp>")
- 基本的に無視していい？？


    pit_stop_area.position.x: 89626.3671875
    pit_stop_area.position.y: 43134.921875
    pit_stop_area.position.z: 42.10000228881836
    pit_stop_area .orientation.x: 0.0
    pit_stop_area.orientation.y: -0.0
    pit_stop_area.orientation.z: -0.878817200660705
    pit_stop_area.orientation.w: -0.47715866565704346