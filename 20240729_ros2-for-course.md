# [Autoware入門講座](https://automotiveaichallenge.github.io/aichallenge-documentation-2024/course/index.html)を実施するためのROS2最小インストール手順

## 手順の概要
### 1度だけ実行すればよい手順
1. [自動運転AIチャレンジの環境構築](https://automotiveaichallenge.github.io/aichallenge-documentation-2024/setup/requirements.html)を完了させる
2. [Autoware入門講座の環境構築](https://automotiveaichallenge.github.io/aichallenge-documentation-2024/course/index.html#_2)にあるように、[ROS2 Humbleの公式手順](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html)に沿ってROS2をインストールする
### 毎回実行する必要がある手順
- `source /opt/ros/humble/setup.bash`

## ROS2 Humbleの公式手順のうち、1度だけ実行すれば良い手順の詳細
- [Setup Sources](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html#setup-sources)の中の
  - "Now add the ROS 2 GPG key with apt."の、以下
    - `sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg`
      - これは長いので、改行で分割されないように、コピー&ペーストし、実行する
      - これで、ROS2パッケージの鍵が登録される
  - "Then add the repository to your sources list."の、以下
    - `echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null`
      - これは長いので、改行で分割されないように、コピー&ペーストし、実行する
      - これで、ROS2パッケージのリポジトリが登録される
- [Install ROS 2 packages](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html#install-ros-2-packages)の中の
  - "Update your apt repository caches after setting up the repositories."の、以下
    - `sudo apt update`
      - これで、パッケージ一覧が最新化される
  - "ROS 2 packages are built on frequently updated Ubuntu systems. It is always recommended that you ensure your system is up to date before installing new packages."の、以下
    - `sudo apt upgrade`
      - これで、パッケージ全体が更新される
  - "Desktop Install (Recommended): ROS, RViz, demos, tutorials."の、以下
    - `sudo apt install ros-humble-desktop`
      - これで、ROS2がインストールされる
  - "Development tools: Compilers and other tools to build ROS packages"の、以下
    - `sudo apt install ros-dev-tools`
      - これで、ROS2の開発ツールがインストールされる

## ROS2 Humbleの公式手順のうち、シェル起動後に、毎回手動で実行する必要がある手順の詳細
- [Environment setup](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html#environment-setup)の、[Sourcing the setup script](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html#sourcing-the-setup-script)の、"Set up your environment by sourcing the following file."の、以下
  - `source /opt/ros/humble/setup.bash`
    - これを実行しないと、`ros2`コマンドなどを実行した際に、`ros2: command not found`などと返される
    - `~/.bashrc`などに、`source /opt/ros/humble/setup.bash`を追記することで、毎回手動で実行することを避けることができる
   
## ここまで実行したら
- あとは`ros2`コマンドなどでROS2を楽しむだけ!
   
## おまけ: aptによるupgrade
- ROS2のインストールという観点では、`sudo apt update`と`sudo apt upgrade`は1度実施すれば良いのですが、脆弱性対応や不具合修正という観点では、日常的に`sudo apt update`と`sudo apt upgrade`を実施しておいたほうが良いかと思います
  - まれに更新することにより問題が起こる場合もありますが、逆に問題が直る場合もあるかと思います
  - 最新状態で実行できない場合は、後からインストールした参加者も同じことになっている可能性が高いので、他のメンバーや運営に相談しましょう
