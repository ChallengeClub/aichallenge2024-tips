# 走行経路最適化で絶望日記 2024/07/24

# 情報
- 元記事: https://zenn.dev/tamago117/articles/b021d2fcb875cc
- 元リポジトリ: https://github.com/tamago117/AIchallenge2023_racetrajectory_optimization
# pip3 install
- `pip3 install -r requirements.txt` -> エラー多発 -> 絶望
## numpy〜trajectory_planning_helpers
- Ubuntu 22.04のPythonは3.10.2 vs リポジトリの[numpy==1.18.1](https://pypi.org/project/numpy/1.18.1/)はPython3.5〜3.8までのサポート?
  - requirements.txtでnumpy==1.22.4にすると、trajectory_planning_helpersまでは入る
    - 22.04以降で一番古いバージョン
    - numpy2系はAPIが大きく変わったと聞いた
## casdi以降
- [casadi==3.5.1](https://pypi.org/project/casadi/3.5.1/)はPython２〜3.6までのサポート?
  - requirements.txtによると`# the following is required for minimum time optimization only`とのことなので、trajectory_planning_helpersまで入れば、とりあえずは動く?
# 地図の入力形式
- 元リポジトリでは、csvが入力フォーマットとなっている
  - 2023大会では、osm以外にcsvがある
    - https://github.com/AutomotiveAIChallenge/aichallenge2023-racing/tree/main/docker/aichallenge/aichallenge_ws/src/aichallenge_submit/aichallenge_submit_launch/map/sample_scripts/outline
  - 2024大会では、osmしかない
    - https://github.com/AutomotiveAIChallenge/aichallenge-2024/tree/main/aichallenge/workspace/src/aichallenge_submit/aichallenge_submit_launch/map
  - -> どうしたら変換できるもの?
