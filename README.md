# jq芸の練習

[JSON Example](https://json.org/example.html)から使えそうなサンプルを借りてくる。

`[]`で配列になっているjson

```
❯ cat menu.json | jq '.menu.items[].id'
"Open"
"OpenNew"
null
"ZoomIn"
"ZoomOut"
"OriginalView"
null
"Quality"
"Pause"
"Mute"
null
"Find"
"FindAgain"
"Copy"
"CopyAgain"
"CopySVG"
"ViewSVG"
"ViewSource"
"SaveAs"
null
"Help"
"About"
```


## References
- [シェル芸で使いたい jqイディオム \- Qiita](https://qiita.com/nmrmsys/items/5b4a4bd2e3909db161b1)
- [JSON Example](https://json.org/example.html)