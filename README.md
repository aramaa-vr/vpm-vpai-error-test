# VPAI導入時における「Spatializer Settings Updated」ダイアログの発生検証報告書

## 1. 検証の概要
VPAI（VPM Package Auto Installer）を使用してパッケージを展開した際、Unityエディタ上で「Spatializer Settings Updated」ダイアログが表示される挙動について、最小構成の環境を作成し、再現性と発生条件を検証した。

---

## 2. 再現環境 (Environment)

### ソフトウェア・パッケージ構成
| 項目 | バージョン / 詳細 |
| :--- | :--- |
| **Unity Editor** | 2022.3.22f1 |
| **VRChat SDK - Base** | 3.10.0 (最新より1マイナーバージョン下を初期設定) |
| **VRChat SDK - Avatars** | 3.10.0 (最新より1マイナーバージョン下を初期設定) |
| **VRChat Package Resolver Tool** | 0.1.29 |
| **VPMPackageAutoInstaller** | 1.1.5 |
| **Modular Avatar** | 1.16.2 |
| **NDMF** | 1.11.0 |

### サーバー側設定 (Remote Config)
検証用に以下のリポジトリおよびパッケージを構成した。
(作成時のVRChat SDKバージョンは、最新のものに更新させるために3.10.1を指定しています。)

* **VPM Repository:** [vpm-vpai-error-test.json](https://github.com/aramaa-vr/vpm-repos/blob/master/develop/vpm-vpai-error-test.json)
```json
{
	"name": "aramaa.vpm-vpai-error-test",
	"id": "io.github.aramaa.vpm-vpai-error-test",
	"author": "aramaa",
	"url": "https://aramaa-vr.github.io/vpm-repos/develop/vpm-vpai-error-test.json",
	"packages": {
		"jp.aramaa.vpm-vpai-error-test": {
			"versions": {
				"1.0.0": {
					"name": "jp.aramaa.vpm-vpai-error-test",
					"version": "1.0.0",
					"url": "https://github.com/aramaa-vr/vpm-vpai-error-test/releases/download/1.0.0/jp.aramaa.vpm-vpai-error-test-1.0.0.zip?",
					"displayName": "vpm-vpai-error-test",
					"description": "vpm-vpai-error-test",
					"unity": "2022.3",
					"unityRelease": "22f1",
					"documentationUrl": "",
					"changelogUrl": "",
					"licensesUrl": "",
					"license": "Custom",
					"author": {
						"name": "aramaa"
					},
					"vpmRepositories": [
						"https://vpm.nadena.dev/vpm.json"
					],
					"vpmDependencies": {
						"nadena.dev.modular-avatar": ">=1.16.2",
						"com.vrchat.avatars": ">=3.10.1"
					},
					"type": "avatar"
				}
			}
		}
	}
}
```

* **Package ZIP:** [jp.aramaa.vpm-vpai-error-test-1.0.0.zip](https://github.com/aramaa-vr/vpm-vpai-error-test/releases/download/1.0.0/jp.aramaa.vpm-vpai-error-test-1.0.0.zip)
* **Package JSON:** [package.json (Raw)](https://raw.githubusercontent.com/aramaa-vr/vpm-vpai-error-test/refs/heads/master/package.json)
```json
{
    "name": "jp.aramaa.vpm-vpai-error-test",
    "version": "1.0.0",
    "url": "https://github.com/aramaa-vr/vpm-vpai-error-test/releases/download/1.0.0/jp.aramaa.vpm-vpai-error-test-1.0.0.zip?",
    "displayName": "vpm-vpai-error-test",
    "description": "vpm-vpai-error-test",
    "unity": "2022.3",
    "unityRelease": "22f1",
    "documentationUrl": "",
    "changelogUrl": "",
    "licensesUrl": "",
    "license": "Custom",
    "author": {
        "name": "aramaa"
    },
    "vpmRepositories": [
        "https://vpm.nadena.dev/vpm.json"
    ],
    "vpmDependencies": {
        "nadena.dev.modular-avatar": ">=1.16.2",
        "com.vrchat.avatars": ">=3.10.1"
    },
    "type": "avatar"
}
```

---

## 3. VPAI 設定内容
検証パッケージに含まれる `com.anatawa12.vpm-package-auto-installer/config.json` の内容は以下の通り。

```json
{
    "vpmDependencies": {
        "jp.aramaa.vpm-vpai-error-test": "1.x.x"
    },
    "vpmRepositories": [
        "https://aramaa-vr.github.io/vpm-repos/develop/vpm-vpai-error-test.json",
        "https://vpm.nadena.dev/vpm.json"
    ]
}

```

---

## 4. 検証手順と結果

### 検証手順

1. Unity 2022.3.22f1 にて新規プロジェクトを作成。
2. あえて旧バージョンの VRChat SDK (3.10.0) を事前にインストールし、バージョン更新が走る余地を作る。
3. 作成した VPAI パッケージをプロジェクトにインポートし、展開を開始。

### 検証結果

VPAIによるパッケージ展開（および依存関係の解決）の過程で、以下のダイアログが発生することを確認した。

> **Spatializer Settings Updated**  
> *VRChat SDK detected incorrect Audio Spatializer  
>  settings and corrected them.  
> For the changes to fully apply - you need to restart  
> your editor.*  

---

## 5. 結論と考察

本事象は、VPAIによるパッケージ導入プロセスにおいて VRChat SDK がロード（またはアップデート）された際、プロジェクトの `Audio Settings` における **Spatializer Plugin** が未設定（またはデフォルト）であることをSDK側が検知し、自動修正を試みたために発生するものである。

VPAI自体の不具合ではなく、VRChat SDKの標準的な初期設定フローがVPAIの展開プロセス中にトリガーされたことによる「仕様通りの挙動」であると判断できる。
