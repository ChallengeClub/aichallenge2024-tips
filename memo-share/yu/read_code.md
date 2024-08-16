# コード解読のメモです。
AICHALLENG-2024/aichallenge/workspace/srcフォルダには主に以下２つのフォルダで構成されている。
- aichallenge_system : ros描画の設定、aichallenge_submitの起動コマンドなどが記載されていて、今回の対象外となる
- aichallenge_submit : 今回の主な作業対象で、rosの各nodeがここに記載されている。Autoware-Microのノード図の各ノード、ノード間のトピックがの定義が以下のファイルで記載されている
```
aichallenge-2024/aichallenge/workspace/src/aichallenge_submit/aichallenge_submit_launch/launch/reference.launch.xml
```
reference.launch.xmlのフォーマットは[ROS 2 launchのXMLフォーマット](https://docs.ros.org/en/foxy/Tutorials/Intermediate/Launch/Creating-Launch-Files.html)となっていて、読み方は公式ドキュメントなどを参考。

各ノードのコメントなどが書かれているので、まずはこちらのコメント単位でコードを読んで行く。

### Localization
##### Node: imu_gnss_poser
方位（imu情報）とGNSSの情報を受け取り、車両位置をekf_localizer用のフォーマットに変換しているだけで、多分変更不要なところだと思う。
```
aichallenge-2024/aichallenge/workspace/src/aichallenge_submit/imu_gnss_poser/src/imu_gnss_poser_node.cpp
```

##### Node: gyro_odometer
車速履歴と方位（imu情報）の情報を受取、車両向きをkf_localizer用のフォーマットに変換している。Autowareディフォルトのモジュールを利用している。

##### Node: ekf_localizer
[Extend Kalman Filter Localizer](https://autowarefoundation.github.io/autoware.universe/main/localization/ekf_localizer/)
というライブラリーを使用して、姿勢とGNSS情報で位置推定を行っている。設定値を設定しているが、多分現状開発は不要。設定したトピックで関係ありそうなものを以下にリストアップします。

- 出力トピック(要確認)

出力がekf_localizerに使用される。
| トピック | 概要 |
----|---- 
| /localization/kinematic_state | 計算した車両位置、速度、向き |

- そのた入力パラメータ(要確認)
全部ディフォルト値になっていて、多分センサーモジュールとチュニックが行われいない？

| トピック | 概要 |
----|---- 
| tf_rate | 位置更新頻度が５０Hzと設定されている |

##### Node: twist2accel
ekf_localizerの情報をもとに、ノイズを除去して、加速度を正確に推定する

### Planning
##### Node: mission_planner
Autowareの標準モジュール[mission_planner](https://autowarefoundation.github.io/autoware.universe/pr-2609/planning/mission_planner/)で地図情報と位置情報からルートを計算。今回は固定のコースなので、調整することが不要かも。

##### Node: behavior_path_planner
Autowareの標準モジュール[behavior_path_planner](https://autowarefoundation.github.io/autoware.universe/main/planning/behavior_path_planner/autoware_behavior_path_planner/)です。すでに障害物を避ける機能が入っていますが、ドキュメントによるとセンターライン付近の障害物をよけれませんので、今回の大会の障害物避けはできないなさそうです。また現状では[dummy_perception_publisher]から空Object情報を受信していている。

##### Node: path_to_trajectory
もともとはbehavior_path_plannerから出力した情報をフォーマット変換していいただけですが、これをお試しに障害物避けを試しているところです。


### Map
##### Node: lanelet2_map_loader
地図データは以下のファイルに設定されていて、読み込みは「Lanelet」というライブラリーが使われている。このモジュールが主に画面表示用で、経路計画への影響は調査中。
```
aichallenge-2024/aichallenge/workspace/src/aichallenge_submit/aichallenge_submit_launch/map/lanelet2_map.osm
```
[Lanelet](https://tech.tier4.jp/entry/2021/06/23/160000#%E8%87%AA%E5%8B%95%E9%81%8B%E8%BB%A2%E3%81%AE%E5%9C%B0%E5%9B%B3)はこちらのサイトを読めば地図がわかるようになる。

[Lanelet official site](https://fzi-forschungszentrum-informatik.github.io/Lanelet2/)

走行経路などはこちらのマップから編集が来ます。
[edit map](https://qiita.com/Massy0127/items/9a646d6b8e1c33f8dace)

障害物もマップ情報に追加すべき？


### create our python module
##### error info 
error:
```
EasyInstallDeprecationWarning: easy_install command is deprecated. Use build and pip and other standards-based tools.
```
solution
```
pip install setuptools==58.2.0
```