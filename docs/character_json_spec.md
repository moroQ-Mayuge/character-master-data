# キャラクターJSON仕様書

## 1. 目的

キャラクターガチャで生成されたキャラクターを、Git管理・検索・画像生成・Web図鑑・将来的なゲーム実装へ流用しやすい形式で保存する。

基本方針は以下とする。

- 1キャラ1JSON。
- ガチャで表示した文章をそのまま保持する。
- 検索やツール連携用に構造化データも保持する。
- 三面図・一枚絵などのアセット参照を後から追加できる。
- 仕様変更に備えてスキーマバージョンを持つ。

## 2. 推奨保存パス

```text
characters/{year}/{event_or_pickup}/{character_id}.json
```

例:

```text
characters/2026/summer_festival/aoi_reina.json
characters/2026/deep_sea_explorer/kamishiro_shiori.json
```

## 3. トップレベル構造

```json
{
  "metadata": {},
  "gacha": {},
  "display": {},
  "structured": {},
  "tags": {},
  "assets": {},
  "generation": {},
  "notes": []
}
```

## 4. metadata

管理用メタデータ。

```json
{
  "metadata": {
    "schema_version": "1.0.0",
    "character_id": "2026-000001",
    "slug": "aoi_reina",
    "created_at": "2026-07-08T00:00:00+09:00",
    "updated_at": "2026-07-08T00:00:00+09:00",
    "generator": "Character Gacha Master Chat",
    "specification_version": "4.1",
    "language": "ja"
  }
}
```

### 必須項目

- `schema_version`
- `character_id`
- `slug`
- `created_at`
- `generator`
- `specification_version`

## 5. gacha

ガチャ排出時の情報。

```json
{
  "gacha": {
    "rarity": "SSR",
    "pickup_theme": "水着・ビーチの夏祭り",
    "event_name": "サマーフェスティバル2026",
    "time_theme": "夕方・ビーチステージ前広場",
    "ticket_before": 259,
    "ticket_cost": 1,
    "ticket_after": 258,
    "draw_count": 1,
    "animation_title": "SUMMER FESTIVAL GACHA",
    "animation_text": "ガチャ演出本文",
    "is_weekly_first_draw": false,
    "weekly_bonus_ticket": 0
  }
}
```

## 6. display

チャット上で表示した内容をそのまま保存する。

```json
{
  "display": {
    "character_info_line": "キャラ情報：...",
    "danbooru_tags_line": "girl, {{{original, summer festival}}}, ...",
    "one_comment": "一言紹介",
    "rarity_label": "SSR",
    "title": "トロピカルドリンクスタンド店長",
    "introduction_text": "任意の補足紹介"
  }
}
```

### 方針

- `character_info_line` はガチャ出力の一行キャラ情報をそのまま保存する。
- `danbooru_tags_line` はガチャ出力の一行タグをそのまま保存する。
- 表示内容の原本として扱う。

## 7. structured

検索・ツール連携用に、キャラ情報を構造化する。

```json
{
  "structured": {
    "name": "蒼井レイナ",
    "full_name": "蒼井レイナ",
    "full_name_reading": "あおいれいな",
    "nickname": "サンドクイーン",
    "job": "ビーチバレーボール選手兼エキシビションマッチキャプテン",
    "age": 27,
    "species": "人間",
    "attribute": "夏",
    "appearance": "自信に満ちた爽やかな笑顔とアスリートらしい凛々しい雰囲気",
    "eyes": "サファイアブルーの切れ長の瞳",
    "hair": "ダークネイビーのハイポニーテール、白いスポーツリボン",
    "body_type": "長身でしなやかなアスリート体型",
    "bust_impression": "普通",
    "body_features": "健康的な小麦色の肌と引き締まった筋肉",
    "first_person": "私",
    "user_call": "みなさん",
    "others_call": "○○さん",
    "personality": "勝負好きだがフェアプレーを重んじる",
    "speech_style": "明るく力強い",
    "ending": "〜いきましょう！",
    "principle": "スポーツの楽しさを伝えること",
    "social_tendency": "初心者にも丁寧に教える",
    "catchphrase_habit": "ナイスプレーです！",
    "favorite": "アサイーボウル",
    "weak_subject": "準備運動不足",
    "outfit": "ホワイトとネイビーのスポーツビキニ、ホワイトのアームスリーブ、ネイビーのスポーツサンバイザー、ホワイトのビーチソックス",
    "equipment": "公式ビーチバレーボール、キャプテンホイッスル、チームタオル",
    "skills": ["ビーチバレーボール", "コーチング", "イベント進行"],
    "special_skill": "サンドストームスパイク",
    "weakness": "負けず嫌いでつい練習しすぎる",
    "secret": "大会後は必ず全員で記念写真を撮る",
    "remarks": "サマーフェスティバル・エキシビションマッチ優勝候補"
  }
}
```

## 8. tags

画像生成AI向けタグを保存する。

```json
{
  "tags": {
    "danbooru": "girl, {{{original, summer festival}}}, {{{modern, 27 years old}}}, {{average bust}}, tall athletic build, lightly tanned skin, sapphire blue sharp eyes, dark navy high ponytail, {{{white and navy sports bikini, white arm sleeves, navy sports sun visor, white beach socks}}}, {{{official beach volleyball, captain whistle, team towel}}}",
    "tag_source": "character_info",
    "rules_version": "2.0",
    "contains_basic_tags": false,
    "policy_safe": true
  }
}
```

### ダンボールタグ生成ルール

- 一行のみ。
- 説明無し。
- 半角カンマ区切り。
- 画像化できない情報はタグ化しない。
- キャラ情報に無い内容を追加しない。
- 重複タグ禁止。
- `1girl` や `solo` 等の基本タグは使用しない。
- ポリシー違反となるタグ表記は行わない。
- 先頭は必ず `girl,` とする。

### タグ順

```text
girl,
{{{original, 世界観}}},
{{{年代, 年齢 years old}}},
{{胸サイズ}},
体特徴,
目特徴,
髪特徴,
{{{服装全体, 上半身服装, 腰部服装, 首元及び肩, 手服装, 頭服装, 装飾品, 靴下等足装備, 靴}}},
{{{衣装以外の持ち物}}}
```

### タグ化しない情報

- 性格
- 一人称
- 二人称
- 口調
- 語尾
- 好物
- 苦手
- 趣味
- 秘密
- 備考
- 呼び方
- 行動原理
- 対人傾向
- 口癖
- 設定のみの能力説明

## 9. assets

画像・プロンプト・関連ファイルの参照。

```json
{
  "assets": {
    "turnaround": {
      "path": "images/turnaround/2026/summer_festival/aoi_reina_turnaround.png",
      "status": "not_generated"
    },
    "illustration": {
      "path": "images/illustrations/2026/summer_festival/aoi_reina_card.png",
      "status": "not_generated"
    },
    "thumbnail": {
      "path": "images/thumbnails/2026/summer_festival/aoi_reina.png",
      "status": "not_generated"
    }
  }
}
```

`status` の例:

- `not_generated`
- `generated`
- `needs_retry`
- `approved`
- `rejected`

## 10. generation

生成時の補足情報。

```json
{
  "generation": {
    "source_chat": "ChatGPT",
    "model_note": "manual_gacha_generation",
    "policy_note": "全年齢向け。水着イベントは健康的なスポーツ・レジャー表現として処理。",
    "style_note": "ソフトライティング、アニメ公式イラスト風、ノイズなし、ギラつきなし。",
    "turnaround_prompt_note": "三面図では必要に応じてパーカー、パレオ、ラッシュガード等を組み合わせる。",
    "illustration_prompt_note": "一言紹介とイベントテーマを元にゲームカード品質で制作。"
  }
}
```

## 11. notes

任意のメモ。

```json
{
  "notes": [
    "初回登録",
    "三面図未作成",
    "夏イベント限定衣装"
  ]
}
```

## 12. 最小JSON例

```json
{
  "metadata": {
    "schema_version": "1.0.0",
    "character_id": "2026-000001",
    "slug": "example_character",
    "created_at": "2026-07-08T00:00:00+09:00",
    "generator": "Character Gacha Master Chat",
    "specification_version": "4.1",
    "language": "ja"
  },
  "gacha": {
    "rarity": "R",
    "pickup_theme": "水着・ビーチの夏祭り",
    "time_theme": "朝・ビーチ",
    "ticket_cost": 1
  },
  "display": {
    "character_info_line": "キャラ情報：...",
    "danbooru_tags_line": "girl, ...",
    "one_comment": "..."
  },
  "structured": {
    "name": "example"
  },
  "tags": {
    "danbooru": "girl, ...",
    "tag_source": "character_info",
    "rules_version": "2.0"
  },
  "assets": {},
  "generation": {},
  "notes": []
}
```
