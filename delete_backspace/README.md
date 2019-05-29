# Karabiner-Elementsでctrl + comma をbackspace、ctrl + periodをdelete (fn + backspace) としてリマップ

## はじめに
`ctrl + hjkl` でVim風のカーソル移動を設定すると、`ctrl + h (backspace)`と`ctrl + k (カーソルより後ろの文字列を切り取り）`が使えなくなります。

`ctrl + k`は、頻繁に使わないので`shift + end`と`ctrl + x` で良いのですが、`ctrl + h`については右上`backspace`キーはホームポジションから遠く、そこに戻りたくはありませんでした。ホームポジションから近いキーで代用できないか検討することにしました。

またmacからwindowsを操作する上でそもそも`control + h`で`backspace`ではなく、置換windowが出てしまうアプリも多く、macとwinで操作方法に統一感がない状態になっていました。

幸いにもmacもwinにも`ctrl + comma/period`は大した機能が割り当てられてなさそうなので、それぞれ`backspace`と`delete`を割り当てることにしました。


## 導入方法
[こちら](https://github.com/imoris/karabiner-elements-settings/blob/master/delete_backspace/delete_backspace.json)に設定ファイルは置いてあります。
1. jsonファイルをDLして以下に格納してください。
`~/.config/karabiner/assets/complex_modifications`
1. Karabiner-ElementsのPreferences画面を開き、Complex Modificationsタブを選択してください。
1. Add ruleを選択し、`ctrl comma to backspace and ctrl period to delete`をenableしてください。

