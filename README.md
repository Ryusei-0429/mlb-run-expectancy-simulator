# mlb-run-expectancy-simulator

MLB Stats API とマルコフ連鎖を用いて、野球における得点期待値計算と打順最適化を研究するプロジェクトです。

## 研究目的

- 打者ごとの打席結果を確率分布としてモデル化する
- イニングをマルコフ連鎖として表現し、状態遷移を評価する
- 打順ごとの得点期待値・得点確率分布を比較する
- 期待値最大の打順候補を探索する

## 研究課題

1. 打席結果（アウト・単打・二塁打・三塁打・本塁打・四球・死球・犠飛・併殺）の確率推定
2. 状態（アウト数・塁状況・打順位置）に基づく遷移行列の構築
3. 解析解（マルコフ連鎖）とモンテカルロ法の整合性検証
4. 打順最適化（上位候補の比較を含む）
5. 再現性・実験条件・使用データの保存

## 前提方針（要点）

- 実データ（API取得）と研究用仮定データを明確に分離する
- 乱数使用時はシードを指定可能にする
- API 取得日時・エンドポイント・パラメータを記録する
- 単純化したモデル仮定は `docs/assumptions.md` に明記する

## 推奨ディレクトリ構成

```text
mlb-run-expectancy-simulator/
├── README.md
├── pyproject.toml
├── .gitignore
├── src/
│   └── mlb_simulator/
│       ├── __init__.py
│       ├── api_client.py
│       ├── data_loader.py
│       ├── models.py
│       ├── probabilities.py
│       ├── transitions.py
│       ├── markov.py
│       ├── simulator.py
│       ├── lineup.py
│       ├── analysis.py
│       └── visualization.py
├── tests/
│   ├── test_api_client.py
│   ├── test_probabilities.py
│   ├── test_transitions.py
│   ├── test_markov.py
│   ├── test_simulator.py
│   └── test_lineup.py
├── notebooks/
├── data/
│   ├── raw/
│   ├── processed/
│   └── README.md
├── results/
├── docs/
│   ├── research_method.md
│   ├── assumptions.md
│   ├── experiment_log.md
│   ├── markov_minimum_issue_draft.md
│   └── design_open_questions.md
└── .github/
    ├── ISSUE_TEMPLATE/
    │   ├── feature_request.md
    │   ├── bug_report.md
    │   └── research_task.md
    └── pull_request_template.md
```

## 次の実装ステップ

- `docs/assumptions.md` の仮定に基づき、状態遷移関数の最小実装を作成
- 主要テスト（確率合計=1、3アウト終了、再現性など）を追加
- モデル結果を CSV/JSON/Markdown で出力可能にする
