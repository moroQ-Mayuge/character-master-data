# character-master-data

オリジナルキャラクターガチャ企画のマスターデータ管理リポジトリです。

このリポジトリでは、キャラクターガチャで生成されたキャラクター情報、ダンボールタグ、ガチャ演出情報、三面図・一枚絵などのアセット参照を、JSONとドキュメントで継続管理します。

## 目的

- キャラクター設定の蓄積
- ガチャ演出・レアリティ・ピックアップ履歴の管理
- 画像生成AI向けダンボールタグの保存
- 三面図・一枚絵などのアセット管理
- 将来的なWeb図鑑、ゲーム実装、検索ツールへの流用

## 基本構成

```text
character-master-data/
├── README.md
├── docs/
│   ├── character_gacha_spec.md
│   ├── character_json_spec.md
│   └── repository_structure.md
├── templates/
│   └── character_template.json
├── characters/
├── events/
├── images/
│   ├── turnaround/
│   └── illustrations/
├── prompts/
└── tags/
```

## 現行仕様

- ガチャ仕様: `docs/character_gacha_spec.md`
- キャラクターJSON仕様: `docs/character_json_spec.md`
- リポジトリ構成: `docs/repository_structure.md`
- JSONテンプレート: `templates/character_template.json`

## 運用方針

キャラクターは原則として1キャラ1JSONで保存します。表示用の一行キャラ情報・ダンボールタグをそのまま保持しつつ、検索やツール連携に使いやすい構造化データも併せて保存します。
