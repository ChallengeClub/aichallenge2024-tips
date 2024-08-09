# 経路計画で絶望日記 2024/08/09

# [AIchallenge2023_racetrajectory_optimization](https://github.com/tamago117/AIchallenge2023_racetrajectory_optimization)が入らない
- Ubuntuを22.04から20.04にしたら、基本解決した
  - requirements.txtを修正しなくてもそのまま入る
  - 画面表示もあるので、UbuntuはServerではなくDesktop

# 基本構造
- osm -> csvは提供無し
  - 2023大会はgitリポジトリにcsvが入っているが、それはAWSIM開発の中で生成されたもの
  - 2024大会はcsv提供無し -> 質問会でアドバイスのあった、iASLチームによりSlackで共有されていたものを使用
- ai_challenge_converter.pyとmain_globaltraj.pyの2段階実行
  - ai_challenge_converter.pyで、innteとouterのcsvからmain_globaltraj.py用のcsvに変換
    - innteとouterのcsvはそれぞれ、converted_inner_track_line.csvとconverted_outer_track_line.csvとしてハードコーディング
      - -> トップディレクトリにそれぞれの名前で設置
    - main_globaltraj.py用のcsvは、inputs/tracks/ai_challenge.csvに出力される
      - ai_challenge.csvは、innerとouter、及びそこから算出される中心線が入っている?
  　　　　- ai_challenge_converter.pyは、画面表示無し
  - main_globaltraj.pyは、画面表示あり
    - -> sshからではなくデスクトップで実行

# ai_challenge_converter.pyの実行
- pandasが必要
  - pandas2はAPI非互換と聞いた
  - -> 日付が近そうな1.1系で最新のpandas-1.1.5をpip install
- csvの列数が合わない
  - 2023大会のcsvと比較して、yawが無さそう
    - yawは使用されていなさそう
    - -> ai_challenge_converter.pyの`column_names = ['x', 'y', 'z', 'yaw']`からyawを削除

# main_globaltraj.pyの実行
## エラーその1 quadprogがundefined symbol
```
tomo-v@ai-cpu-u2004:~/AIchallenge2023_racetrajectory_optimization$ python3 main_globaltraj.py
Traceback (most recent call last):
  File "main_globaltraj.py", line 1, in <module>
    import opt_mintime_traj
  File "/home/tomo-v/AIchallenge2023_racetrajectory_optimization/opt_mintime_traj/__init__.py", line 1, in <module>
    import opt_mintime_traj.src
  File "/home/tomo-v/AIchallenge2023_racetrajectory_optimization/opt_mintime_traj/src/__init__.py", line 1, in <module>
    import opt_mintime_traj.src.opt_mintime
  File "/home/tomo-v/AIchallenge2023_racetrajectory_optimization/opt_mintime_traj/src/opt_mintime.py", line 7, in <module>
    import trajectory_planning_helpers as tph
  File "/home/tomo-v/.local/lib/python3.8/site-packages/trajectory_planning_helpers/__init__.py", line 23, in <module>
    import trajectory_planning_helpers.opt_min_curv
  File "/home/tomo-v/.local/lib/python3.8/site-packages/trajectory_planning_helpers/opt_min_curv.py", line 3, in <module>
    import quadprog
ImportError: /home/tomo-v/.local/lib/python3.8/site-packages/quadprog.cpython-38-x86_64-linux-gnu.so: undefined symbol: _Z7qpgen2_PdS_PiS0_S_S_S_S_S_S0_S0_S0_S0_S0_S0_S_S0_
```
- -> trajectory_planning_helpers>=0.76で入る最新の0.79のまま、quadprog>=0.1.9を入れると解決するっぽい

## エラーその2 main_globaltraj.pyがcould not convert string to float: ''
```
tomo-v@ai-cpu-u2004:~/AIchallenge2023_racetrajectory_optimization$ python3 main_globaltraj.py
Traceback (most recent call last):
  File "main_globaltraj.py", line 206, in <module>
    reftrack_imp = helper_funcs_glob.src.import_track.import_track(imp_opts=imp_opts,
  File "/home/tomo-v/AIchallenge2023_racetrajectory_optimization/helper_funcs_glob/src/import_track.py", line 26, in import_track
    csv_data_temp = np.loadtxt(file_path, comments='#', delimiter=',')
  File "/home/tomo-v/.local/lib/python3.8/site-packages/numpy/lib/npyio.py", line 1159, in loadtxt
    for x in read_data(_loadtxt_chunksize):
  File "/home/tomo-v/.local/lib/python3.8/site-packages/numpy/lib/npyio.py", line 1087, in read_data
    items = [conv(val) for (conv, val) in zip(converters, vals)]
  File "/home/tomo-v/.local/lib/python3.8/site-packages/numpy/lib/npyio.py", line 1087, in <listcomp>
    items = [conv(val) for (conv, val) in zip(converters, vals)]
  File "/home/tomo-v/.local/lib/python3.8/site-packages/numpy/lib/npyio.py", line 794, in floatconv
    return float(x)
ValueError: could not convert string to float: ''
```

- -> ChatGPTの分析によりai_challenge_converter.pyで出力されるinputs/tracks/ai_challenge.csvに、''を含む行がある
- -> 手動で削除

＃ main_globaltraj.pyの表示結果で絶望
![image](https://github.com/user-attachments/assets/066e2517-c415-45ce-ab88-333a1cb68379)

- -> innerが表示されていない -> csvを要確認
- -> outerがつながっていない -> ''を手動削除した部分?
