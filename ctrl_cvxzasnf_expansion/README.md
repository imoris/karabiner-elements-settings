# ctrl_cvxzasnf_extension
## はじめに
MacbookとParallelsによる仮想化Windowsを併用しており、Macbook側の操作とWindows操作の統一感を得るため、Karabiner-Elementsを使ってMacbookの操作をcontrolキーでも行えるようにしました。
Apple信者にキレられそうですが、cmdキーよりcontrolキーの方が押しやすいですよね！

## 導入方法
[こちら]()に設定ファイルは置いてあります。
1. jsonファイルをDLして以下に格納してください。
`~/.config/karabiner/assets/complex_modifications`
1. Karabiner-ElementsのPreferences画面を開き、Complex Modificationsタブを選択してください。
1. Add ruleを選択し、`Change left_control + CXVZSAWFN to left_command + CXVZSAWFN ver 4`をenableしてください。

## Keymappingした項目
以下が全てcmdキーの代わりにcontrolを利用することができるようにしました。
- cmd + c : コピー
- cmd + v : 貼り付け
- cmd + x : 切り取り
- cmd + z : Undo
- cmd + a : 全選択
- cmd + s : 保存
- cmd + n : 新規window
- cmd + f : 検索 


## 例外アプリケーション
ctrl + c / ctrl + aが使えないと困るので以下は一部のキーについてKeymappingしないこととしました。
- iTerm2
- Terminal

以下はそもそもkeymappingが必要ないので例外としました。
- Parallels関連
- VMWare関連

## 制約事項
VS CodeやCloud 9のようにTerminalが同じwindowでくっついてきてしまうやつはどうしようもないです。このときばかりはkeymapをoffにして使っています。