# JIS to US(ANSI) keyboard remapping with Karabiner-Elements

## はじめに
私の勤め先ではリモートワークを行う際にはVPN接続の上、VMWare Horizon Clientからサーバ上の仮想デスクトップにアクセスする必要があります。
接続先の仮想デスクトップ（Windows 10)が曲者で、サーバー上での管理をやりやすくするためか多くの制限が課されています。
例えば管理者権限がないため、新しいソフトウェアをインストールできなかったり、レジストリの値を書き換えることもできません。  
デフォルトでは日本語のハードウェアキーボードレイアウトにはJISキーボードが設定されているのですが、それをUS(ANSI)キーボードにすることができません。通常であればハードウェアキーボードレイアウトの変更で対応できるのですが、WindowsのVerが古いためかそのオプションが出てこないという仕様になっています。唯一できることとしては、Englishの言語パックを入れてキーボードタイプをANSIにすることですが、それだけ英語だけしかUSキーボードに対応できません（しかも日本語IMEと英語IMEをWin+Spaceでいちいち切り替える必要がある）。  
そのためWindows上でゴニョゴニョするのは諦め、Macbook上でKarabiner-Elementsのcomplex modificationsの機能を使ってRemapすることとしました。

## 環境
Parallels => 仮想化win10 => VMW HC => 仮想デスクトップサーバwin10　という接続となっており、仮想化win10の方でKeymapを変えることとしました。 
### 実機
- Macbook Pro 2017 (mac OS 10.14.4 mojave)
- HHKB Professional 2 type-s (US配列)
- Parallels Desktop 14

### 接続元仮装マシン
- Windows 10 (Ver 1809)
- VMWare Horizon Client 4.5.0

### 接続先仮想デスクトップ
- Windows 10 (ver 1709)


## 導入方法
[こちら](https://github.com/imoris/karabiner-elements-settings/blob/master/swap_jp_us_layout/swap_jp_us_layout.json)に設定ファイルは置いてあります。
1. jsonファイルをDLして以下に格納してください。
`~/.config/karabiner/assets/complex_modifications`
1. Karabiner-ElementsのPreferences画面を開き、Complex Modificationsタブを選択してください。
1. Add ruleを選択し、`Remap Japanese Keyboard to US custom for Win (日本語環境)`をenableしてください。


## Remapの設定
- Karabiner-Elementsのgithubのissueにちょうど類似のTopicがあがっていましたので、[こちら](https://github.com/tekezo/Karabiner-Elements/issues/167#issuecomment-331133220)の設定を使わせてもらうことにしました
- 上記の設定をそのまま使うと私の環境では以下が発生していました
    - `hyphen + shift (underscore)`が`"\"(backslash)`になる
    - `backslash`および`backslash + shift (pipe)`が`"]"(close_bracket)`になる
    - `grave_accent_and_tilde (backquote)`および`grave_accent_and_tilde + shift (tilde)`が`半角/全角キー`になる
- これを修正するため以下のようにKeymappingを若干修正および追加を行いました。  
    (1)  hyphen + shift が underscoreになるように修正
    ``` json
    "from": {
        "key_code": "hyphen",
        "modifiers": {
            "mandatory": [
                "shift"
            ],
            "optional": [
                "caps_lock"
            ]
        }
    },
    "to": [
        {
            "key_code": "international1",
            "modifiers": [
                "left_shift"
            ]
        }
    ]
    ```

    (2) backslash およびbackslash + shift (pipe) の追加
    ``` json
    "from": {
        "key_code": "backslash"
    },
    "to": [
        {
            "key_code": "international1"
        }
    ]
    ```
    ``` json
    "from": {
        "key_code": "backslash",
        "modifiers": {
            "mandatory": [
                "shift"
            ],
            "optional": [
                "caps_lock"
            ]
        }
    },
    "to": [
        {
            "key_code": "international3",
            "modifiers": [
                "left_shift"
            ]
        }
    ]
    ```

    (3) backquoteとtildeの追加

    ``` json
    "from": {
        "key_code": "grave_accent_and_tilde",
        "modifiers": {
            "optional": [
                "any"
            ]
        }
    },
    "to": [
        {
            "key_code": "open_bracket",
            "modifiers": [
                "left_shift"
            ]
        }
    ]
    ```

    ``` json
    "from": {
        "key_code": "grave_accent_and_tilde",
        "modifiers": {
            "mandatory": [
                "shift"
            ],
            "optional": [
                "caps_lock"
            ]
        }
    },
    "to": [
        {
            "key_code": "equal_sign",
            "modifiers": [
                "left_shift"
            ]
        }
    ]
    ```

- またParallels(もしくはVMWare Horizon)かつHHKB Pro2 (US配列)のみで今回のKeymapを有効にしたかったので以下の設定の入れました。
    ``` json
    "conditions": [
        {
            "type": "frontmost_application_if",
            "bundle_identifiers": [
                "^com\\.parallels\\.desktop\\.console",
                "^com\\.vmware\\.horizon"
            ]
        },
        {
            "type": "device_if",
            "identifiers": [
                {
                    "vendor_id": 2131,
                    "product_id": 256
                }
            ]
        }
    ]
    ```
- すべての設定を記載したjsonは[こちら](https://github.com/imoris/karabiner-elements-settings/blob/master/swap_jp_us_layout/swap_jp_us_layout.json)に置いてあります。


## 設定を終えて
少し修正しただけですが、日本語キーボードの入力コードをKarabiner-ElementsのEvent Viewerで確認して、HHKBの入力コードから入れ替えるのは、とても頭が混乱しました。Windowsで普通にUSキーボードが使えるようになって非常に仕事がしやすくなりました（当たり前）。おそらく同じ悩みを抱えている方はあまりいないと思うのですが、この記事が少しでも役立てば幸いです。

## 参考
- [Karabiner-Elementsの設定項目をまとめました](https://qiita.com/s-show/items/a1fd228b04801477729c)
- [Karabiner-Elements Offical Manual](https://pqrs.org/osx/karabiner/document.html)
- [github issue: change Japanese keyboard to US(JIS to ANSI) #167](https://github.com/tekezo/Karabiner-Elements/issues/167)