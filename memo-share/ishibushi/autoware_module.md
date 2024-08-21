# Obstacle Cruise Planner
### できること
- 経路近くに静的障害物がある場合に停止する。
- 自己の前に動的障害物がある場合に巡航する。
- 経路近くに静的または動的障害物がある場合に減速する。

# Mission Planner
### できること
- 現在の位置から目標位置までの経路を計算する。
- 経路は静的な地図に基づくレーンの連続で構成される。
- 動的な障害物や地図の変化（例：工事によるレーンの閉鎖）は考慮しない。
- 出力トピックは、目標位置やチェックポイントが設定された時のみ更新される。
### システムの柔軟性
- 地図の形式に依存しない。
- 現在のAutoware.universeでは、Lanelet2形式の地図プラグインのみがサポートされている。
### MRMのルート管理
- MRM（Mission Replanning and Management）は、自動運転システムにおけるミッションの再計画と管理を担当する機能
- 通常の状態とMRMの状態に応じて、ルートのリクエストと計画結果を配信。

## Path optimizer