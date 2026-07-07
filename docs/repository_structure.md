# リポジトリ構成仕様

## 推奨構成

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
│   └── {year}/
│       └── {event_or_pickup}/
│           └── {character_slug}.json
├── events/
│   └── {year}/
│       └── {event_slug}.json
├── images/
│   ├── turnaround/
│   │   └── {year}/
│   │       └── {event_or_pickup}/
│   ├── illustrations/
│   │   └── {year}/
│   │       └── {event_or_pickup}/
│   └── thumbnails/
│       └── {year}/
│           └── {event_or_pickup}/
├── prompts/
│   ├── turnaround/
│   └── illustrations/
└── tags/
```

## ディレクトリ説明

### `docs/`

仕様書を管理する。

- `character_gacha_spec.md`: ガチャ運用・キャラ生成・画像生成方針
- `character_json_spec.md`: キャラクターJSONの構造
- `repository_structure.md`: リポジトリ構成

### `templates/`

JSONやプロンプトのテンプレートを管理する。

### `characters/`

キャラクターJSONを保存する。

原則として1キャラ1JSON。

```text
characters/2026/summer_festival/aoi_reina.json
```

### `events/`

イベントやピックアップテーマの情報を保存する。

例:

```text
events/2026/summer_festival_2026.json
```

### `images/`

画像アセットを保存する。

- `turnaround/`: 三面図
- `illustrations/`: 一枚絵、カードイラスト
- `thumbnails/`: 図鑑用サムネイル

### `prompts/`

画像生成用プロンプトや再生成用メモを保存する。

### `tags/`

タグ変換ルール、タグ一覧、分類表などを保存する。

## ファイル命名規則

### キャラクターJSON

```text
{character_slug}.json
```

例:

```text
aoi_reina.json
kamishiro_shiori.json
```

### 三面図

```text
{character_slug}_turnaround.png
```

### 一枚絵

```text
{character_slug}_card.png
```

### サムネイル

```text
{character_slug}_thumb.png
```

## character_slug ルール

- 小文字英数字とアンダースコアを使用する。
- 日本語名はローマ字化する。
- 同名が出た場合は連番を付ける。

例:

```text
aoi_reina
uminase_serina
shirahama_marina
```

## Git運用

### 1キャラ追加時のコミット例

```text
Add character: Aoi Reina
```

### 仕様更新時のコミット例

```text
Update gacha specification
Update character JSON schema
```

### 画像追加時のコミット例

```text
Add turnaround image: Aoi Reina
Add card illustration: Aoi Reina
```

## 運用メモ

- 仕様書は `docs/` を正とする。
- キャラクターJSONは `characters/` を正とする。
- 画像ファイルはJSONの `assets` にパスを記録する。
- ガチャ出力の原文は `display` に保持する。
- 検索やツール利用に必要な情報は `structured` に保持する。
