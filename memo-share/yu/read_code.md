# コード解読のメモです。
AICHALLENG-2024/aichallenge/workspace/srcフォルダには主に以下２つのフォルダで構成されている。
- aichallenge_submit : 今回の主な作業対象で、rosの各nodeがここに記載されている
- aichallenge_system : ros描画の設定、aichallenge_submitの起動コマンドなどが記載されていて、今回の対象外となる

### 地図について
地図データは以下のファイルに設定されていて、読み込みは「Lanelet」というライブラリーが使われている。
```
aichallenge-2024/aichallenge/workspace/src/aichallenge_submit/aichallenge_submit_launch/map/lanelet2_map.osm
```
「Lanelet」はこちらのサイトを読めば地図がわかるようになる。
https://tech.tier4.jp/entry/2021/06/23/160000#%E8%87%AA%E5%8B%95%E9%81%8B%E8%BB%A2%E3%81%AE%E5%9C%B0%E5%9B%B3
