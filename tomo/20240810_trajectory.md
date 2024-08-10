# 経路計画で絶望日記 2024/08/10
以下は全て、ChatGPTへのお願いを間違えてDiscordに書いてしまい恥ずかしいのをごまかすための記述です。

# iaslのへやで共有されていたcsv
- ChatGPTでプロット -> コースになっていそう

<img width="400" alt="image" src="https://github.com/user-attachments/assets/fad4c0fe-754b-4ba0-ae38-2458037e5d22">

# ai_challenge_converter.pyで生成されたai_challenge.csvのx_mとy_mを合成
- 元のcsvのinnerとouterの行数が異なり、50ポイント分足らない
  - -> このずれがコースの中心の計算を狂わせている?
- 課題
  - 中心線が環状につながっていない
  - コースをはみ出している
  - コース幅も正しく計算されていない可能性

<img width="400" alt="image" src="https://github.com/user-attachments/assets/85ebdbea-d0c7-402c-83f6-3d6c26c4142d">

# ChatGPTにリサンプルさせてみた
- だいぶ良くなったけど、コース前半はまだずれる
- 算出した中心線が、人間感覚的に中心線になってはじめて、最適経路が算出できると想定

<img width="400" alt="image" src="https://github.com/user-attachments/assets/60777ae0-fb46-4011-a73d-023f0247ab37">

# 次の一手
- 中心線が描けるようにリサンプルをがんばる
- ai_challenge_converter.pyの目的は、innnerとouterから、中心線とコース幅を算出することと思われる
- 中心線データが別途共有されているのなら、中心線データをそのまま使い、コース幅を一定としてしまうとか?
  - 見た目上、コース幅が一定に思える
  - 街を歩きながら考えて思いついた

# 中心線データをそのままに、コース幅3.5固定でやってみた
- 赤いひげのようなものは、コースの幅を示していて、コースのカーブ具合によって生える方向が変わる模様
  - この赤いひげがクロスするとだめなのか…
  - -> 手動編集しか道はないのか…?

<img width="400" alt="image" src="https://github.com/user-attachments/assets/169d7453-3b2e-464b-9ece-d5e4b87ace73">
