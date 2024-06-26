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

### 02. 速度計画 

### 03. 障害物回避 
