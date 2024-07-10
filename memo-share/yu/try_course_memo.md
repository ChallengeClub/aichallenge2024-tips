# 公式サイトの講座を試して、ノーハウを共有していきましょう

### 00. 環境構築

#### 遭遇したエラー
##### python 'empy' NOT FOUND
 ```
colcon build --symlink-install

```
を実行時に発生するエラーで、empyがディフォルトでグローバル環境にあり、ローカル環境にないため、以下のコマンドでインストール必要がある。
```
pip3 install -U empy
# ローカル環境にemがある場合削除する必要がある
# rm ~/.local/lib/python3.10/site-packages/em.py
```

### 01. 車両インターフェース 
編集対象ファイルはsrc/autoware_practice_course/src/vehicle/forward.cppにあります。

#### 遭遇したエラー

##### ros2: command not found
rosインストール済みでけど、パスがうまく設定てきてないと発生します。
ターミナルが複数利用することが多く、~/.bashrcに追記したほうが便利。
```
source /opt/ros/humble/setup.bash
```

##### Package 'autoware_practice_course' not found
違うTerminalでROS2コマンドを実行しようとすると、発生する。
ターミナルが複数利用することが多く、~/.bashrcに追記したほうが便利。
```
source install/setup.bash
```

### 02. 速度計画 

### 03. 障害物回避 
