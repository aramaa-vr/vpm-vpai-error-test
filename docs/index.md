# あらまあ素敵なショップ unitypackage 導入ガイド

> **対象**: `jp.aramaa.何か-x.x.x-installer.unitypackage` を導入する方
>
> **最重要ポイント**: **unitypackage の導入前に、VRChat SDK（Avatars / Base）を先に最新化**してください。

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Compatible-brightgreen)](#) [![Unity](https://img.shields.io/badge/Unity-Setup%20Guide-000000)](#) [![VRChat SDK](https://img.shields.io/badge/VRChat%20SDK-Required-4b8bbe)](#)

---

## 目次

- [このガイドでできること](#このガイドでできること)
- [最短フロー（3ステップ）](#最短フロー3ステップ)
- [1. VRChat SDK を最新にする（必須）](#1-vrchat-sdk-を最新にする必須)
- [2. unitypackage を導入する](#2-unitypackage-を導入する)
- [3. エラーが出たときの復旧手順](#3-エラーが出たときの復旧手順)
- [復旧しない場合の追加対応（優先度順）](#復旧しない場合の追加対応優先度順)
- [FAQ（よくある質問）](#faqよくある質問)
- [最終チェックリスト](#最終チェックリスト)

---

## このガイドでできること

- 導入前にやるべき SDK 更新の順序を確認できる
- unitypackage 導入時の分岐（`VRChat SDK - Avatars` 表示時）に対応できる
- `Spatializer Settings Updated` 発生時の復旧を完了できる

---

## 最短フロー（3ステップ）

| Step | 作業 | 目安時間 | 完了条件 |
|---|---|---:|---|
| 1 | VRChat SDK を最新化 | 2〜5分 | `Avatars` / `Base` が最新 |
| 2 | unitypackage を導入 | 1〜3分 | `Import` / `Install` が完了 |
| 3 | エラー時の復旧 | 5〜15分 | Console エラーが解消 |

---

## 1. VRChat SDK を最新にする（必須）

> [!IMPORTANT]
> **このステップを先に実施しないと、導入時の不整合やコンパイルエラーの原因になります。**

1. VCC で対象プロジェクトの `Manage Project` をクリック
2. `VRChat SDK - Avatars` を最新に更新
3. `VRChat SDK - Base` を最新に更新
4. 対象プロジェクトの `Open Project` をクリック

![SDK 更新前の例](assets/images/sdk-version-before-update-exp.avif)

### チェックポイント

- `VRChat SDK - Avatars` が最新
- `VRChat SDK - Base` が最新
- 更新後のプロジェクトを開いている

---

## 2. unitypackage を導入する

1. `jp.aramaa.何か-x.x.x-installer.unitypackage` をダブルクリック
2. 1回目のダイアログで `Import` をクリック
3. 2回目のダイアログで `Install` をクリック

![Import ダイアログの例](assets/images/flow-01-import.avif)

### 分岐: `VRChat SDK - Avatars` が表示された場合

> [!WARNING]
> `Cancel` をクリックし、**先に「1. VRChat SDK を最新にする（必須）」**を実施してください。

![Install ダイアログの例](assets/images/flow-02-install-exp.avif)

---

## 3. エラーが出たときの復旧手順

`Spatializer Settings Updated` が表示された場合は、以下を順番に実施してください。

1. `RestartLater` をクリック
2. **Unity を閉じる（保存して終了）**
3. VCC で対象プロジェクトの `Manage Project` を開く
4. `Resolve` をクリック
5. `VRChat SDK - Avatars` を最新に更新
6. `VRChat SDK - Base` を最新に更新
7. 必要に応じて VPAI を再導入
8. Unity を再起動し、Console エラー消失を確認

![Save and Restart](assets/images/flow-04-reset-later.avif)

![Manage Packages](assets/images/flow-08-manage-packages.avif)

---

## 復旧しない場合の追加対応（優先度順）

| 優先度 | 対応 | 補足 |
|---|---|---|
| 高 | VCC で SDK を一度 `Remove` して再インストール | 依存関係を初期化しやすい |
| 中 | `Library` フォルダを削除して Unity 再起動 | 再インポートに時間がかかる |
| 中 | `Packages/manifest.json` の依存関係を確認 | バージョン衝突の切り分け |

---

## FAQ（よくある質問）

<details>
<summary><strong>Q. 先に unitypackage を入れてしまいました。やり直しは必要ですか？</strong></summary>

A. Console エラーがない場合はそのまま進められることがあります。エラーがある場合は「3. エラーが出たときの復旧手順」を実施してください。

</details>

<details>
<summary><strong>Q. `Resolve` してもエラーが消えません。</strong></summary>

A. 「復旧しない場合の追加対応（優先度順）」を上から順に試してください。特に SDK の再インストールで解決するケースが多いです。

</details>

<details>
<summary><strong>Q. なぜ Avatars と Base の両方を更新する必要がありますか？</strong></summary>

A. 片方のみ更新すると依存関係がずれ、導入時に不整合が起きる可能性があるためです。

</details>

---

## 最終チェックリスト

- [ ] `VRChat SDK - Avatars` が最新
- [ ] `VRChat SDK - Base` が最新
- [ ] unitypackage の `Import` / `Install` が完了
- [ ] Unity Console のエラーが解消

---

## 補足

- 本手順は「VCC 推奨」と明記された商品向けです。
- 本ドキュメントは GitHub Pages（標準 Markdown / HTML レンダリング）で崩れにくい記法を使用しています。
