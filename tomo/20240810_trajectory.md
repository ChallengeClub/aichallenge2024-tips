# 経路計画で絶望日記 2024/08/10

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
- 
<img width="400" alt="image" src="https://github.com/user-attachments/assets/60777ae0-fb46-4011-a73d-023f0247ab37">

