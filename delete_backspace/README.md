# Karabiner-Elementsでctrl + comma をbackspace、ctrl + periodをdelete (fn + backspace) としてリマップ

## はじめに
ctrl hjkl でVim風のカーソル移動を設定すると、ctrl h (backspace)とctrl k (カーソルより後ろの文字列を切り取り）が使えなくなります。

ctrl kは、頻繁に使わないのでshift + end で良いのですが、ctrl hについては右上backspaceキーはホームポジションから遠く、そこに戻りたくはありませんでした。ホームポジションから近いキーで代用できないか検討することにしました。

またmacからwindowsを操作する上でそもそもcontrol + hでdeleteではなく、置換windowが出てしまうアプリも多く、macとwinで操作方法に統一感がない状態になっていました。

幸いにもmacもwinにもctrl + comma/periodは大した機能が割り当てられてなさそうなので、それぞれbackspaceとdeleteを割り当てることにしました。


## 導入方法
[こちら](https://github.com/imoris/karabiner-elements-settings/blob/master/delete_backspace/delete_backspace.json)に設定ファイルは置いてあります。
1. jsonファイルをDLして以下に格納してください。
`~/.config/karabiner/assets/complex_modifications`
1. Karabiner-ElementsのPreferences画面を開き、Complex Modificationsタブを選択してください。
1. Add ruleを選択し、`Change left_control + CXVZSAWFN to left_command + CXVZSAWFN ver 4`をenableしてください。

