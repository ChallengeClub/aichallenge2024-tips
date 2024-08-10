# パラメータをconfig に集約する。
### 目的
- config に初期パラメータを集約することで管理がしやすくなる
- 変更時にコンパイルが不要になる
## 手順
1. nodeのソースコード内で以下の関数でパラメータを宣言
```
this->declare_parameter("パラメータ名", 初期値)
```
- 例)
```
this->declare_parameter("minimum_trj_point_size", 10)
```

2. nodeのソースコード内で以下の関数でパラメータを設定
```
変数名 = this->get_parameter("パラメータ名").as_int();
```
- ※doubole型の場合は .as_double() にする

例)
```
minimum_trj_point_size_ = this->get_parameter("minimum_trj_point_size").as_int();
```
3. yamlの作成
```
/**:
  ros__parameters:
    パラメータ名: 設定値
```
例)
```
/**:
  ros__parameters:
    minimum_trj_point_size: 10
```
4. yaml 用のconfig ファイルを作成
- package にconfig フォルダを作成し、yaml ファイルを保存する。
 
5. 対象のノードを実行しているlaunch ファイル内でconfigを指定
```
<param from="$(find-pkg-share パッケージ名)/config/yamlファイル名"/>
```
- 例
```
<param from="$(find-pkg-share simple_pure_pursuit)/config/default_simple_pure_pursuit.yaml"/>
```
6. cmakelist に記載
```
ament_auto_package(
  INSTALL_TO_SHARE
  config
  )
```