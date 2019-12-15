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

長さやtypeを知りたいとき

```
❯ cat menu.json | jq '.menu.items | length'
22

❯ cat menu.json | jq '.menu.items | type'
"array"

❯ cat menu.json | jq '.menu.items[] | type'
"object"
"object"
"null"
"object"
"object"
"object"
"null"
"object"
"object"
"object"
"null"
"object"
"object"
"object"
"object"
"object"
"object"
"object"
"object"
"null"
"object"
"object"
```

keyを知りたいとき

```
❯ cat menu.json | jq '.menu.items[] | keys'
[
  "id"
]
[
  "id",
  "label"
]
jq: error (at <stdin>:76): null (null) has no keys
```


## References
- [シェル芸で使いたい jqイディオム \- Qiita](https://qiita.com/nmrmsys/items/5b4a4bd2e3909db161b1)
- [JSON Example](https://json.org/example.html)