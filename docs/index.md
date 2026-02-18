# あらまあ素敵なショップ配布 Unitypackage 導入時の注意点

> 対象: `jp.aramaa.何か-x.x.x-installer.unitypackage` のような名前のパッケージを入れる場合の注意

## 先に結論（重要3点）

1. **Unitypackage 実行前に、VRChat SDK を最新化する**
2. インポート中のダイアログに **VRChat SDK が見えたらキャンセル**する
3. 誤って入れた場合は、**VCC で SDK を再インストールして復旧**する

---

## 1) VRChat SDK を最新にしてからパッケージを入れる

VPAI 導入前に、必ず VCC 側で VRChat SDK を最新化してください。

![SDK 更新前の例](assets/images/sdk-version-before-update-exp.avif)

1. VCCで対象プロジェクトの`Manage Project`をクリック
2. `VRChat SDK - Avatars` を最新に更新
3. `VRChat SDK - Base` を最新に更新
4. 対象プロジェクトを`Open Project`をクリック
5. `jp.aramaa.何か-x.x.x-installer.unitypackage` をダブルクリック

## 2) ダイアログに VRChat SDK が出たらキャンセル

インポート時に VRChat SDK 関連項目が表示された場合は、そのまま進めず **いったんキャンセル**してください。

![Import ダイアログの例](assets/images/flow-01-import.avif)

- VRChat SDK を unitypackage 側から同時導入しない
- 先に VCC で SDK 状態を整える
- その後、VPAI 導入を再実行

> VRChat SDK の管理は VCC で行うのが安全です。

## 3) 誤って VRChat SDK を入れてしまったときの復旧

以下の手順で復旧してください。

1. **Unity を閉じる（保存して終了）**
2. VCC で対象プロジェクトを開く
3. `Manage Project` から VRChat SDK を **Reinstall / Repair**
4. 必要なら VPAI を再導入
5. Unity を再起動して Console エラー消失を確認

復旧フローの画面例:

- Save and Restart

![Save and Restart](assets/images/flow-04-save-and-restart.avif)

- Enter Safe Mode → Exit Safe Mode → Exit Anyway

![Enter Safe Mode](assets/images/flow-05-enter-safe-mode.avif)
![Exit Safe Mode](assets/images/flow-06-exit-safe-mode.avif)
![Exit Anyway](assets/images/flow-07-exit-anyway.avif)

- 最終確認 OK

![Final OK](assets/images/flow-08-final-ok.avif)

### 復旧しない場合の追加対応

- VCC で SDK を一度 Remove 後に再インストール
- `Library` フォルダ削除後に Unity 再起動（再インポート）
- `Packages/manifest.json` の依存関係を確認

---

## Booth zip 同梱向けのおすすめ運用

- zip 内の目立つ場所に本ページへのリンク（またはショートカット）を置く
- ファイル名を `00_最初に読む_導入注意.md` のようにして先頭表示にする
- 商品説明にも「導入前にこのページを確認」と一文入れる

これで、`jp.aramaa.何か-x.x.x-installer.unitypackage` の誤操作をかなり減らせます。
