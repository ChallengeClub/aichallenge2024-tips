## ROS2でPythonのパッケージを作ってみました

## 作ったもの
https://github.com/shrimp-f/aichallenge-2024/tree/develop/add_sample_pkg/aichallenge/workspace/src/aichallenge_submit/my_package_python

## かんたんなROSのソースコードの管理の説明
ROSは、いくつかの「ノード」というソースコードの塊を「パッケージ」というもので包むような形でソースコードを扱っています。

## パッケージの作成の参考サイト
Creating a package

https://docs.ros.org/en/foxy/Tutorials/Beginner-Client-Libraries/Creating-Your-First-ROS2-Package.html

## パッケージ作成の手順
1. autowareのdockerコンテナの中に入ります
1. $ cd /home/ubuntu/aichallenge-2024/aichallenge/workspace/src/aichallenge_submit
1. $ ros2 pkg create --build-type ament_python my_package_python
1. $ vim /home/ubuntu/aichallenge-2024/aichallenge/workspace/src/aichallenge_submit/my_package_python/my_package_python/main.py でコードを作成します(コンテナの中からだと作成できなかったので、ホスト側で作成するのがよいかもです)
  - (例)https://github.com/shrimp-f/aichallenge-2024/blob/develop/add_sample_pkg/aichallenge/workspace/src/aichallenge_submit/my_package_python/my_package_python/main.py

## パッケージ作成後の設定
- setup.pyの'console_scripts'のところに作ったpythonコードをnodeとして登録します。下記のようなフォーマットです。
{ノード名(任意)} = {パッケージ名}.{ファイル名}:{関数名}
  - (例)
'my_package_python_node = my_package_python.main:main'
https://github.com/shrimp-f/aichallenge-2024/blob/develop/add_sample_pkg/aichallenge/workspace/src/aichallenge_submit/my_package_python/setup.py#L23

## ノード実行と確認の手順
1. autowareのdockerコンテナの中に入ります
1. $ sudo ip link set multicast on lo
1. $ cd /home/ubuntu/aichallenge-2024/aichallenge/workspace/src/aichallenge_submit
1. $ colcon build
1. $ ros2 run my_package_python my_package_python_node
1. 別のターミナルを開いて、docker exec -it {コンテナの名前} bash　でコンテナの中に入ります
1. $ ros2 topic echo /sample_msg すると「hello world」という文字が流れます

## こんなエラーが出たら
ros2 run my_package_python my_package_python_node
を実行すると下記のようなエラーが出ました
```
ros2: selected interface "lo" is not multicast-capable: disabling multicast
```

解決策です。こちらのコマンドをすると治りました。(いしぶしさん、ご教授ありがとうごさいます！)
```
sudo ip link set multicast on lo
```

