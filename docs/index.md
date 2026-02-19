# unitypackage 導入クイックガイド（エラー回避版）

> 対象: `jp.aramaa.何か-x.x.x-installer.unitypackage` を導入する人
>
> **最重要:** `unitypackage` を入れる前に、必ず `VRChat SDK - Avatars` と `VRChat SDK - Base` を最新化する。

---

## まずやること（30秒確認）

- 「VCC 推奨」商品なら、可能なら **VCC 導入を優先**
- 今回は unitypackage で進める
- 先に SDK を更新してから Import する

---

## 手順（この順で実施）

### 1) VRChat SDK を更新する（必須）

1. VCC で対象プロジェクトの `Manage Project` を開く
2. `VRChat SDK - Avatars` を更新
3. `VRChat SDK - Base` を更新
4. `Open Project` で開く

![SDK 更新前の例](assets/images/sdk-version-before-update-exp.avif)

**完了条件**
- `Avatars` が最新
- `Base` が最新

---

### 2) unitypackage を導入する

1. `jp.aramaa.何か-x.x.x-installer.unitypackage` をダブルクリック
2. 1つ目のダイアログで `Import`
3. 2つ目のダイアログで `Install`

![Import ダイアログの例1](assets/images/flow-01-import.avif)
![Import ダイアログの例2](assets/images/flow-02-install-true.png)

**もし `VRChat SDK - Avatars` が表示されたら**
- `Cancel` を押す
- 手順1（SDK 更新）を先に完了してからやり直す

![Install ダイアログの例](assets/images/flow-02-install-exp.avif)

---

### 3) VCC でアップデート可能な状態にする

1. VCC を再起動
2. `Settings → Packages → Installed Repositories` で `aramaa` にチェック
3. `Projects → (対象プロジェクト) → Manage Project → Selected Repos → Multiple Repositories → aramaa` にチェック

![VCCのInstalled Repositoriesでaramaaチェックを確認する画面]({{ "/assets/images/vrcc_repo_opt_q82.webp" | relative_url }})
![Unityでインポートが完了した画面]({{ "/assets/images/install-unitypackage-done.webp" | relative_url }})

---

## エラーが出たとき（`Spatializer Settings Updated`）

以下を **上から順に** 実施してください。

1. `RestartLater` をクリック
2. Unity を閉じる（保存して終了）
3. VCC で対象プロジェクトの `Manage Project` を開く
4. `Resolve` をクリック
5. `VRChat SDK - Avatars` を更新
6. `VRChat SDK - Base` を更新
7. 必要なら VPAI を再導入
8. Unity 再起動後、Console エラーが消えたか確認

![Save and Restart](assets/images/flow-04-reset-later.avif)
![Manage Packages](assets/images/flow-08-manage-packages.avif)

---

## まだ直らない場合（追加対応）

1. VCC で SDK を一度 `Remove` して再インストール
2. `Library` フォルダを削除して Unity 再起動
3. `Packages/manifest.json` の依存関係を確認

---

## 最終チェック

- [ ] `VRChat SDK - Avatars` が最新
- [ ] `VRChat SDK - Base` が最新
- [ ] unitypackage の `Import` / `Install` が完了
- [ ] Unity Console のエラーが解消

---

## 注意

- 「VCC 推奨」商品での unitypackage 導入は非推奨
- 本手順は既知ケース向けで、すべての環境での解決を保証するものではありません
