# あらまあ素敵なショップ unitypackage 導入時の注意点

> VCC 推奨と書かれている商品のunitypackage入れる場合は注意が必要です。  
> 対象: `jp.aramaa.何か-x.x.x-installer.unitypackage` のような名前のパッケージを入れる場合の注意  

## 概要

商品によっては他社が作成したものを使用しています。  
そのため、稀に意図しない不具合が発生するのを回避するための手順を説明します。   

1. VRChat SDK を最新にする
2. プロジェクトにパッケージを導入する
3. VRChat SDK を最新に更新し忘れてエラーが出た場合の復旧方法  

---

## 1) VRChat SDK を最新にする

必ず VCC 側で VRChat SDK を最新に更新してください。

![SDK 更新前の例](assets/images/sdk-version-before-update-exp.avif)

1. VCCで対象プロジェクトの`Manage Project`をクリック
3. `VRChat SDK - Avatars` を最新に更新
4. `VRChat SDK - Base` を最新に更新
5. 対象プロジェクトの`Open Project`をクリック


## 2) プロジェクトにパッケージを導入する

`jp.aramaa.何か-x.x.x-installer.unitypackage` をダブルクリック  
`Import`をクリック  

![Import ダイアログの例](assets/images/flow-01-import.avif)

その後に表示されるダイアログで`Install`をクリック 

### もしも `VRChat SDK - Avatars` が表示された場合の対応  
**Cancel**して`1)`の対応をしてください

![Import ダイアログの例](assets/images/flow-02-install-exp.avif)

## 3) VRChat SDK を最新に更新し忘れてエラーが出た場合の復旧方法

以下の手順で復旧してください。

`Spatializer Settings Updated`が出た場合

- RestartLaterをクリック

![Save and Restart](assets/images/flow-04-reset-later.avif)

**Unity を閉じる（保存して終了）**

VCC で対象プロジェクトの`Manage Project` を開く

- Resolveをクリック

![Save and Restart](assets/images/flow-08-manage-packages.avif)

3. `VRChat SDK - Avatars` を最新に更新
4. `VRChat SDK - Base` を最新に更新
5. 必要なら VPAI を再導入
6. Unity を再起動して Console エラー消失を確認

### 復旧しない場合の追加対応

- VCC で SDK を一度 Remove 後に再インストール
- `Library` フォルダ削除後に Unity 再起動（再インポート）
- `Packages/manifest.json` の依存関係を確認
