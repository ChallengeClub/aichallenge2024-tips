# コード解読のメモです。
AICHALLENG-2024/aichallenge/workspace/srcフォルダには主に以下２つのフォルダで構成されている。
- aichallenge_system : ros描画の設定、aichallenge_submitの起動コマンドなどが記載されていて、今回の対象外となる
- aichallenge_submit : 今回の主な作業対象で、rosの各nodeがここに記載されている。Autoware-Microのノード図の各ノード、ノード間のトピックがの定義が以下のファイルで記載されている
```
aichallenge-2024/aichallenge/workspace/src/aichallenge_submit/aichallenge_submit_launch/launch/reference.launch.xml
```
reference.launch.xmlのフォーマットはROS 2 launchのXMLフォーマットとなっていて、読み方は公式ドキュメントなどを参考。

https://docs.ros.org/en/foxy/Tutorials/Intermediate/Launch/Creating-Launch-Files.html

各ノードのコメントなどが書かれているので、まずはこちらのコメント単位でコードを読んで行く。

### Localization
##### Node: imu_gnss_poser
[Extend Kalman Filter Localizer](https://autowarefoundation.github.io/autoware.universe/main/localization/ekf_localizer/)
というライブラリーを使用して、位置推定を行っている。設定値を設定しているが、現状開発は不要。設定したトピックで関係ありそうなものを以下にリストアップします。

- 出力トピック(要確認)
出力がekf_localizerに使用される。
| トピック | 概要 |
----|---- 
| /localization/imu_gnss_poser/pose_with_covariance | 推定位置 |

- そのた入力パラメータ(要確認)
全部ディフォルト値になっていて、多分センサーモジュールとチュニックが行われいない？
| トピック | 概要 |
----|---- 
| tf_rate | 位置更新頻度が５０Hzと設定されている |

##### Node: ekf_localizer

### Map
##### Node: lanelet2_map_loader
地図データは以下のファイルに設定されていて、読み込みは「Lanelet」というライブラリーが使われている。このモジュールが主に画面表示用で、経路計画への影響は調査中。
```
aichallenge-2024/aichallenge/workspace/src/aichallenge_submit/aichallenge_submit_launch/map/lanelet2_map.osm
```
「Lanelet」はこちらのサイトを読めば地図がわかるようになる。
https://tech.tier4.jp/entry/2021/06/23/160000#%E8%87%AA%E5%8B%95%E9%81%8B%E8%BB%A2%E3%81%AE%E5%9C%B0%E5%9B%B3

